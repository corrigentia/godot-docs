.. Generated automatically by doc/tools/makerst.py in Godot's source tree.
.. DO NOT EDIT THIS FILE, but the UndoRedo.xml source instead.
.. The source is found in doc/classes or modules/<name>/doc_classes.

.. _class_UndoRedo:

UndoRedo
========

**Inherits:** :ref:`Object<class_Object>`

**Category:** Core

Brief Description
-----------------

Helper to manage UndoRedo in the editor or custom tools.

Methods
-------

+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :ref:`Variant<class_Variant>`  | :ref:`add_do_method<class_UndoRedo_add_do_method>` **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` method **)** vararg                                         |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`add_do_property<class_UndoRedo_add_do_property>` **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` property, :ref:`Variant<class_Variant>` value **)**     |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`add_do_reference<class_UndoRedo_add_do_reference>` **(** :ref:`Object<class_Object>` object **)**                                                                              |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :ref:`Variant<class_Variant>`  | :ref:`add_undo_method<class_UndoRedo_add_undo_method>` **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` method **)** vararg                                     |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`add_undo_property<class_UndoRedo_add_undo_property>` **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` property, :ref:`Variant<class_Variant>` value **)** |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`add_undo_reference<class_UndoRedo_add_undo_reference>` **(** :ref:`Object<class_Object>` object **)**                                                                          |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`clear_history<class_UndoRedo_clear_history>` **(** :ref:`bool<class_bool>` increase_version=true **)**                                                                         |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`commit_action<class_UndoRedo_commit_action>` **(** **)**                                                                                                                       |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| void                           | :ref:`create_action<class_UndoRedo_create_action>` **(** :ref:`String<class_String>` name, :ref:`MergeMode<enum_UndoRedo_MergeMode>` merge_mode=0 **)**                              |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :ref:`String<class_String>`    | :ref:`get_current_action_name<class_UndoRedo_get_current_action_name>` **(** **)** const                                                                                             |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :ref:`int<class_int>`          | :ref:`get_version<class_UndoRedo_get_version>` **(** **)** const                                                                                                                     |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :ref:`bool<class_bool>`        | :ref:`redo<class_UndoRedo_redo>` **(** **)**                                                                                                                                         |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :ref:`bool<class_bool>`        | :ref:`undo<class_UndoRedo_undo>` **(** **)**                                                                                                                                         |
+--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Enumerations
------------

.. _enum_UndoRedo_MergeMode:

enum **MergeMode**:

- **MERGE_DISABLE** = **0**

- **MERGE_ENDS** = **1**

- **MERGE_ALL** = **2**

Description
-----------

Helper to manage UndoRedo in the editor or custom tools. It works by registering methods and property changes inside 'actions'.

Common behavior is to create an action, then add do/undo calls to functions or property changes, then committing the action.

Here's an example on how to add an action to Godot editor's own 'undoredo':

::

    var undoredo = get_undo_redo() # method of EditorPlugin
    
    func do_something():
        pass # put your code here
    
    func undo_something():
        pass # put here the code that reverts what's done by "do_something()"
    
    func _on_MyButton_pressed():
        var node = get_node("MyNode2D")
        undoredo.create_action("Move the node")
        undoredo.add_do_method(self, "do_something")
        undoredo.add_undo_method(self, "undo_something")
        undoredo.add_do_property(node, "position", Vector2(100,100))
        undoredo.add_undo_property(node, "position", node.position)
        undoredo.commit_action()

:ref:`create_action<class_UndoRedo_create_action>`, :ref:`add_do_method<class_UndoRedo_add_do_method>`, :ref:`add_undo_method<class_UndoRedo_add_undo_method>`, :ref:`add_do_property<class_UndoRedo_add_do_property>`, :ref:`add_undo_property<class_UndoRedo_add_undo_property>`, and :ref:`commit_action<class_UndoRedo_commit_action>` should be called one after the other, like in the example. Not doing so could lead to crashes.

If you don't need to register a method you can leave :ref:`add_do_method<class_UndoRedo_add_do_method>` and :ref:`add_undo_method<class_UndoRedo_add_undo_method>` out, and so it goes for properties. You can register more than one method/property.

Method Descriptions
-------------------

.. _class_UndoRedo_add_do_method:

- :ref:`Variant<class_Variant>` **add_do_method** **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` method **)** vararg

Register a method that will be called when the action is committed.

.. _class_UndoRedo_add_do_property:

- void **add_do_property** **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` property, :ref:`Variant<class_Variant>` value **)**

Register a property value change for 'do'.

.. _class_UndoRedo_add_do_reference:

- void **add_do_reference** **(** :ref:`Object<class_Object>` object **)**

Register a reference for 'do' that will be erased if the 'do' history is lost. This is useful mostly for new nodes created for the 'do' call. Do not use for resources.

.. _class_UndoRedo_add_undo_method:

- :ref:`Variant<class_Variant>` **add_undo_method** **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` method **)** vararg

Register a method that will be called when the action is undone.

.. _class_UndoRedo_add_undo_property:

- void **add_undo_property** **(** :ref:`Object<class_Object>` object, :ref:`String<class_String>` property, :ref:`Variant<class_Variant>` value **)**

Register a property value change for 'undo'.

.. _class_UndoRedo_add_undo_reference:

- void **add_undo_reference** **(** :ref:`Object<class_Object>` object **)**

Register a reference for 'undo' that will be erased if the 'undo' history is lost. This is useful mostly for nodes removed with the 'do' call (not the 'undo' call!).

.. _class_UndoRedo_clear_history:

- void **clear_history** **(** :ref:`bool<class_bool>` increase_version=true **)**

Clear the undo/redo history and associated references.

Passing ``false`` to ``increase_version`` will prevent the version number to be increased from this.

.. _class_UndoRedo_commit_action:

- void **commit_action** **(** **)**

Commit the action. All 'do' methods/properties are called/set when this function is called.

.. _class_UndoRedo_create_action:

- void **create_action** **(** :ref:`String<class_String>` name, :ref:`MergeMode<enum_UndoRedo_MergeMode>` merge_mode=0 **)**

Create a new action. After this is called, do all your calls to :ref:`add_do_method<class_UndoRedo_add_do_method>`, :ref:`add_undo_method<class_UndoRedo_add_undo_method>`, :ref:`add_do_property<class_UndoRedo_add_do_property>`, and :ref:`add_undo_property<class_UndoRedo_add_undo_property>`, then commit the action with :ref:`commit_action<class_UndoRedo_commit_action>`.

.. _class_UndoRedo_get_current_action_name:

- :ref:`String<class_String>` **get_current_action_name** **(** **)** const

Get the name of the current action.

.. _class_UndoRedo_get_version:

- :ref:`int<class_int>` **get_version** **(** **)** const

Get the version, each time a new action is committed, the version number of the UndoRedo is increased automatically.

This is useful mostly to check if something changed from a saved version.

.. _class_UndoRedo_redo:

- :ref:`bool<class_bool>` **redo** **(** **)**

Redo last action.

.. _class_UndoRedo_undo:

- :ref:`bool<class_bool>` **undo** **(** **)**

Undo last action.

