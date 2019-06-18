# Migrating from AZCore to AzCore<a name="lumberyard-migrating-1-5-azcore"></a>

In Lumberyard 1\.5, AzCore replaces AZCore\. In code you will notice this update in AzCore header files:
+ Previously: `#include <AZCore/AZCore/headername.h>`
+ Updated: `#include <AzCore/AzCore/headername.h>`

Update your code to replaces all AZCore references with AzCore\.