=============
Command Flags
=============

Command flags are useful for specifying extra parameters to be used for the processing of a command that doesn't belong
as a command argument.

To create a flag, we first need a builder for flags. We can simply use the ``flags()`` method provided by
``GenericArguments`` to obtain the builder we need. From there, we can specify what type of flag we would like to
create. Note that flags are specified as an argument.

.. code-block:: java
    
    import org.spongepowered.api.command.args.GenericArguments;
    
    .arguments(GenericArguments.flags().flag("s").buildWith(GenericArguments.none()))

This will create a command flag, so that when the player performs ``/our-command -s``, the flag for ``s`` will be true.
Note the ``GenericArguments.none()``. This will prevent the command from having any arguments. If you wish for the
command to have arguments and flags, you will need to specify your arguments within the ``buildWith()`` method.

Now that we have specified that our command may be run with the flag, we can now get the value of the flag. For a
simple boolean flag like the one we have specified above, we can simply just check if it exists. In the example below,
we are checking if the ``args`` for the command has a value for ``s``.

.. code-block:: java
    
    import org.spongepowered.api.text.Text;
    
    if (args.hasAny("s")) {
        src.sendMessage(Text.of("The command flag was specified!"));
    } else {
        src.sendMessage(Text.of("The command flag was not specified."));
    }

Value Flags
===========

Booleans can be great, but what if we wanted flags for things such as strings or integers? This is where value flags
come into play. We simply need to use the ``valueFlag()`` method on our flag builder. Using the ``valueFlag()`` method,
we can specify the type of flag we want to create, such as an integer or string. Creating an integer value flag can be
done like so:

.. code-block:: java
    
    .arguments(GenericArguments.flags().valueFlag(GenericArguments
        .integer(Text.of("value")), "s").buildWith(GenericArguments.none()))

You may replace ``GenericArguments.integer()`` with any other flag type you would like to specify, such as
``GenericArguments.string()``.

Now to retrieve the flag value from our command, we can simply treat it like any other command argument. We simply need
to check if it exists before retrieving it:

.. code-block:: java
    
    Optional<Integer> optional = args.<Integer>getOne("value");
    if(!optional.isPresent()) {
        src.sendMessage(Text.of("The value flag was not specified."));
        return CommandResult.empty();
    }
    int value = optional.get().intValue();
