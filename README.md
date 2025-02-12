# InterwikiDispatcher extension

This is free software licensed under the GNU General Public License. Please
see http://www.gnu.org/copyleft/gpl.html for further details, including the
full text and terms of the license.

## Overview
Adding some simple multi-level interwikis for easier linking to wiki farms.

Hooking into existing interwiki prefixes to provide some limited API support. Subdomain part of the interwiki is validated as `a-z\d-` to avoid open redirect vulnerabilities.

## Example configs
```php
# [[w:c:minecraft]] => https://minecraft.fandom.com/wiki/
# [[w:c:minecraft:Cookie]] => https://minecraft.fandom.com/wiki/Cookie
# [[w:c:de.minecraft:Keks]] => https://minecraft.fandom.com/de/wiki/Keks
$wgIWDPrefixes[] = [
  'interwiki' => 'w', # Interwiki prefix that exists in the interwiki table
  'subprefix' => 'c', # Optional: Subprefix to keep the interwiki working mostly as expected
  'url' => 'https://$2.fandom.com/wiki/$1', # URL format for the interwiki
  'urlInt' => 'https://$2.fandom.com/$3/wiki/$1' # Optional: Additional URL format for the interwiki
];
```
```php
# [[mh:meta]] => https://meta.miraheze.org/wiki/
# [[mh:meta:Miraheze]] => https://meta.miraheze.org/wiki/Miraheze
$wgIWDPrefixes[] = [
  'interwiki' => 'mh',
  'url' => 'https://$2.miraheze.org/wiki/$1'
];
```
```php
# [[farm:mh:meta]] => https://meta.miraheze.org/wiki/
# [[farm:mh:meta:Miraheze]] => https://meta.miraheze.org/wiki/Miraheze
$wgIWDPrefixes[] = [
  'interwiki' => 'farm',
  'subprefix' => 'mh',
  'url' => 'https://$2.miraheze.org/wiki/$1'
];
# [[farm:fd:minecraft]] => https://minecraft.fandom.com/wiki/
# [[farm:fd:minecraft:Cookie]] => https://minecraft.fandom.com/wiki/Cookie
# [[farm:fd:de.minecraft:Keks]] => https://minecraft.fandom.com/de/wiki/Keks
$wgIWDPrefixes[] = [
  'interwiki' => 'farm',
  'subprefix' => 'fd',
  'url' => 'https://$2.fandom.com/wiki/$1',
  'urlInt' => 'https://$2.fandom.com/$3/wiki/$1'
];
# [[farm:gg:terraria]] => https://terraria.wiki.gg/wiki/
# [[farm:gg:terraria:NPCs]] => https://terraria.wiki.gg/wiki/NPCs
# [[farm:gg:de.terraria:NPCs]] => https://terraria.wiki.gg/de/wiki/NPCs
$wgIWDPrefixes[] = [
  'interwiki' => 'farm',
  'subprefix' => 'gg',
  'url' => 'https://$2.wiki.gg/wiki/$1',
  'urlInt' => 'https://$2.wiki.gg/$3/wiki/$1'
];
```