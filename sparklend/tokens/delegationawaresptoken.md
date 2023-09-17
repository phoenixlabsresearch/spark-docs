# DelegationAwareSpToken

The special type of spToken that are minted and burned upon supply and withdraw of assets that has voting power associated _(which can be delegated)_ with them. These _spTokens_ are enabled to delegate voting power of the underlying asset to a different address.

_DelegationAwarespToken_ enables/implements all the methods available for spTokens with additional [`delegateUnderlyingTo`](../../tokens/delegationawarespToken.md#delegateunderlyingto) method.

Refer [_spToken_](sptoken.md) docs for full list of contract api

### delegateUnderlyingTo

`function delegateUnderlyingTo(address delegatee)`

Delegates voting power of the underlying asset to a `delegatee` address.

{% hint style="danger" %}
This method can only be called by `POOL_ADMIN.`
{% endhint %}
