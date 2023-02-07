# DropExtend-1.0
[![Patreon](http://img.shields.io/badge/news%20&%20rewards-patreon-ff4d42)](https://www.patreon.com/jaliborc) [![Paypal](http://img.shields.io/badge/donate-paypal-1d3fe5)](https://www.paypal.me/jaliborc) [![Discord](http://img.shields.io/badge/discuss-discord-5865F2)](https://bit.ly/discord-jaliborc)  

Allows to extend Blizzard dropdowns without spreading taint (because the native dropdown code should not be trusted). Also ensures multiple addons extending the same dropdown through this API do not interfere with one another.

### API
DropExtend provides a single method:

```lua
LibStub('DropExtend-1.0'):Hook(dropdown, callback)
```

- **dropdown:** the frame you wish to extend
- **callback:** function that will be called each time the dropdown native `initFunc` is executed (see [definition](https://wowpedia.fandom.com/wiki/API_UIDropDownMenu_Initialize)), with the same parameters `callback(dropdown, level, menuList)`. Should return a frame you wish to show with the content being initialized, or nil when you have nothing to add.

### Example
This code will add content to the Loot Journal class filter dropdown - one frame `MyMainLevelExtension` to the dropdown main level, and another frame `MyClassListExtension` to the class list:

```lua
LibStub('DropExtend-1.0'):Hook(LootJournalItemsClassDropDown, function(dropdown, level, menuList)
    if level == 1 then
        return MyMainLevelFrame
    elseif level == 2 and UIDROPDOWNMENU_MENU_VALUE == CLASS_DROPDOWN then
        return MyClassListFrame
    end
end)
```

### :warning: Reminder!
If you use this library, please list it as one of your dependencies in the CurseForge admin system. It's a big help! :+1: