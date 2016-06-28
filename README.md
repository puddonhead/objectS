# "objectS" Cross Platform Object Store protocol and utilities
Goal for this project is to create a language agnostic object data format.

The object data (fields/members) are written in nested xml structure:
```xml
<o testObj1 t="org.objectR.MyObject">
  <f t="number">15.0</f>
  <f t="string">test string</f>
  <f t="CDATA"><![CDATA[test cdata]]></f>
  <o memberObj1 t="org.objectR.MemberObj">
    <f t="number">1</f>
  </o>
</o>
```

The goal of this xml is to be as readable as possible, and yet be machine searchable.

Types (attribute 't') of number, string and CDATA are supported. More types are likely to be added to this list.

The choice of using xml of json or other formats was mainly driven by the fact that xml is much more widely used and available everywhere, and that there are many matured tools already available for xml, which is not yet the case for JSON.

Each language (starting with Java) supported by this project will need to create adapters that will need to transform any "bean" object into this xml format. Bean objects will need to be simple, serializable objects. Behaviors can be a part of the bean objects, however the behavior is not persisted to the database. This allows for the code to change over time without significant compatibility issues.

Each language adapter will also need to read this xml, and convert it to the appropriate object based on the type attributes and the data supplied in the xml. Systems written in completely different languages should be able to interchange structured object data using this format aided by a "translation config" file that will tell a .NET based syster, for example, that objects of type "orc.objectR.MyObject" should become "objectR.MyObject" instead. Other than the class definitions of the "bean" classes themselves, the only other config file that may be required in this scenario is the "translation config".
