---
title: Applying a patch takes your site down
labels: Magento Commerce,Magento Commerce Cloud,patch,remove patch,troubleshooting
---

This article talks about the issue where a patch you just applied takes your site down. To resolve it, you can remove the patch.

## Affected products and versions

* Magento Commerce, all supported versions
* Magento Commerce Cloud, all supported versions

## Issue

After you apply a patch, your site goes down.

## Cause

This issue might appear because of a version incompatibility between the patch you just applied to your website, your customizations, other patches you had applied in the past, or some other error.

## Solution

Remove the patch. The method of patch removal is different for Magento Commerce Cloud than for Magento Commerce and Magento Open Source.

### Magento Commerce, Magento Open Source, all 1.X versions

For Magento Commerce and Magento Open Source 1.X versions,

* Run the following SSH command:    ```git    sh SUPEE_patch --revert    ```    

### Magento Commerce, Magento Open Source, all 2.X versions

For Magento Commerce and Magento Open Source 2.X versions,

1. Run the following SSH command:    <pre><code class="language-git">patch -p1 -R <<code>%patch_name%</code>.composer.patch</code></pre>    (If the above command does not work, try using `-p2` instead of `-p1` )
1. For the changes to be reflected, refresh the cache in the Admin under **System** > **Cache Management** .

### Magento Commerce Cloud, all versions

For Magento Commerce Cloud, all versions,

1. Remove the `%patch_name%.composer.patch` file(s) from the `m2-hotfixes` directory.
1. Commit and push your code changes:    ```git    git commit -m "Remove %patch_name%.composer.patch patch" && git push origin    ```    


## Related reading

* [How to apply a composer patch provided by Magento](https://support.magento.com/hc/en-us/articles/360028367731)
* [Apply patches (Magento Commerce Cloud)](https://devdocs.magento.com/guides/v2.3/cloud/project/project-patch.html)
* [How to Apply and Revert \[Magento 1\] Patches](https://devdocs.magento.com/guides/m1x/other/ht_install-patches.html)
