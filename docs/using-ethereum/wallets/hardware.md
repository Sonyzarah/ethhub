;;
;; Related contracts
;;

_ get_proxy() method_id {
    load_base_data();
    return ctx_proxy;
}

_ get_owner() method_id {
    load_base_data();
    return ctx_owner;
}

_ get_controller() method_id {
    load_base_data();
    return ctx_controller;
}

;;
;; Balances for controller
;;

_ get_unowned() method_id {
    load_base_data();
    var [balance, extra] = get_balance();
    return max(balance - owned_balance(), 1);
}

_ get_available() method_id {
    load_base_data();
    return ctx_balance - ctx_balance_sent;
}

;;
;; Pool and staking status
;;

_ get_staking_status() method_id {
    load_base_data();
    load_validator_data();

    var querySent = proxy_stored_query_id != 0;
    var can_unlock = false;
    var until_val = 0;
    if ((proxy_stake_at != 0) & (proxy_stake_until != 0)) {
        until_val = lockup_lift_time(proxy_stake_at, proxy_stake_until, proxy_stake_held_for);
        can_unlock = until_val <= now();
    }
    return (proxy_stake_at, until_val, proxy_stake_sent, querySent, can_unlock, ctx_locked, proxy_stake_lock_final);
}

_ get_pool_status() method_id {
    load_base_data();
    load_member(owner_id());
    return (ctx_balance, ctx_balance_sent, ctx_balance_pending_deposits, ctx_balance_pending_withdraw, ctx_balance_withdraw);
}

;;
;; Params
;;
_ get_params() method_id {
    load_base_data();
    var (enabled, udpates_enabled, min_stake, deposit_fee, withdraw_fee, pool_fee, receipt_price) = ctx_extras;
    return (enabled, udpates_enabled, min_stake, deposit_fee, withdraw_fee, pool_fee, receipt_price);
}

;;
;; Members
;;

_ get_member_balance(slice address) method_id {
    load_base_data();
    load_member(parse_work_addr(address));
    
    member_update_balance();
    return (ctx_member_balance, ctx_member_pending_deposit, ctx_member_pending_withdraw, ctx_member_withdraw);
}

_ get_members_raw() method_id {
    load_base_data();
    return ctx_nominators;
}

_ get_members() method_id {
    load_base_data();

    ;; Init with owner
    load_member(owner_id());
    member_update_balance();
    var list = nil;
    list = cons([ctx_owner, ctx_member_balance, ctx_member_pending_deposit, ctx_member_pending_withdraw, ctx_member_withdraw], list);

    ;; Iterate all members
    var id = -1;
    do {
        (id, var cs, var f) = ctx_nominators.udict_get_next?(256, id);

        ;; NOTE: One line condition doesn't work
        if (f) {
            if (id != owner_id()) {
                ;; For some reason loading member from slice doesn't work
                load_member(id);
                member_update_balance();
                list = cons([serialize_work_addr(id), ctx_member_balance, ctx_member_pending_deposit, ctx_member_pending_withdraw, ctx_member_withdraw], list);
            }
        }
    } until (~ f);

    return list;
}

_ get_member(slice address) method_id {
    load_base_data();
    load_member(parse_work_addr(address));
    member_update_balance();
    return (ctx_member_balance, ctx_member_pending_deposit, ctx_member_pending_withdraw, ctx_member_withdraw);
}

_ supported_interfaces() method_id {
    return (
        123515602279859691144772641439386770278, ;; org.ton.introspection.v0
        256184278959413194623484780286929323492 ;; com.tonwhales.nominators:v0
    );
---
title: Ethereum Hardware Wallets - EthHub

description: Explanation of Ethereum hardware wallets pros and cons as well as a list of vendors.
---

# Hardware

## Summary

Hardware wallets are the most-secure method for accessing your funds while online, as they do not expose your private key to the internet when signing transactions.

## Wallets

* [Ledger](https://shop.ledger.com/pages/ledger-nano-x?r=0fcb4288e45f) - Support for multiple cryptocurrencies and tokens
* [Lattice1](https://gridplus.io/lattice) - Use your Lattice1 as a traditional hardware wallet, set up permissions for spending on the go, or allow recurring payments for subscription services.
* [Trezor](https://shop.trezor.io/product/trezor-model-t?offer_id=15&aff_id=2828) - The original hardware wallet
* [KeepKey](http://keepkey.myshopify.com?afmc=1km&utm_campaign=1km&utm_source=leaddyno&utm_medium=affiliate) - The simple hardware wallet
* [BitBox](https://shop.shiftcrypto.ch/en/products/category/hardware-wallets-1/) - BitBox02 is Swiss engineered minimalist hardware wallet

## Resources

* [Consensys's ethereum-developer-tools-list](https://github.com/ConsenSys/ethereum-developer-tools-list/blob/master/EcosystemResources.md)

