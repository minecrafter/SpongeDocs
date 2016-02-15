===========================
Plugin Defined Translations
===========================

In Sponge, plugin sent messages may be translated to other locales. This way, you may translate your plugin's messages
to other languages, while still being able to support your preferred language.

Player Locales
==============

All of the possible player locales may be found in the ``Locales`` class. Using these locales, you may compare the
player's current locale to the one you wish to provide translations for. This can be done like so:

.. code-block:: java
    
    import org.spongepowered.api.entity.living.player.Player;
    import org.spongepowered.api.text.translation.locale.Locales;
    
    Player player = ...;
    if (player.getLocale() == Locales.EN_PT) {
        player.sendMessage("Arr, this be pirate speak.");
    }

Alternatively, you can use ``NamedLocales``:

.. code-block:: java
    
    import org.spongepowered.api.text.translation.locale.NamedLocales;
    
    Player player = ...;
    if (player.getLocale() == NamedLocales.PIRATE_ENGLISH) {
        player.sendMessage("Arr, this be more a pirate speak.");
    }

*Note:* We should use `else` with our if statement, otherwise only people with Pirate English set as their locale would
ever read our messages!

.. code-block:: java
    
    Player player = ...;
    if (player.getLocale() == NamedLocales.PIRATE_ENGLISH) {
        player.sendMessage("You use a pirate speak!");
    } else {
        player.sendMessage("You do not use a pirate speak! D:");
    }

Translation Helper
==================

Translations Resource Bundle
============================
