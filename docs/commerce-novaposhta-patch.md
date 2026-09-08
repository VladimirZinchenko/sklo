# Commerce Nova Poshta compatibility patch

The project installs the upstream module `drupal/commerce_novaposhta` version
`2.1.0`. A root Composer metadata override is used because the official release
metadata does not describe the Drupal 10 / Commerce 3 dependency set used by
this project. The override keeps the official Drupal.org release archive while
declaring the actual dependencies: Drupal Core `^10`, Drupal Commerce `^3`, and
Commerce Shipping `^3.0`.

A persistent Composer patch is required to keep the module compatible with the
current stack and Nova Poshta API. It fixes ServiceType handling, Commerce 3
compatibility, the PHP 8.4 nullable signature, nullable checkout data, nullable
address element values, the incorrect `region_data` assignment, and adds a
short-lived shipping-rate cache. The patch is stored at
`patches/commerce_novaposhta-2.1.0-commerce3-np-api-php84.patch`, registered in
`patches.json`, and locked by checksum in `patches.lock.json`.

Runtime status:

- `Warehouse` has been verified end-to-end in checkout.
- `Postomat` works for valid Nova Poshta directions.
- `Doors` is currently a fixed-rate service and does not collect a complete
  door-delivery address.
- Creating Nova Poshta waybills (TTN) is outside this patch and requires a
  separate task.

Recovery snapshots created before this work:

- `before-commerce-novaposhta-composer`
- `before-commerce-novaposhta-patch`

After changing the patch, regenerate and review `patches.lock.json`, then verify
with `ddev composer validate --no-check-publish`, `ddev composer patches-doctor`,
and `ddev composer install --dry-run`.
