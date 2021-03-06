---
title: Adding Dependencies to the Configuration-Dependent Data
author: windows-driver-content
description: Adding Dependencies to the Configuration-Dependent Data
ms.assetid: 16e15147-6e83-4675-b050-cf13dcd6b397
keywords:
- GDL WDK , configurations
- configurations WDK GDL , adding dependencies
- adding dependencies to configuration-dependent data WDK GDL
- dependencies in configuration-dependent data WDK GDL
- Switch/Case directive WDK GDL
- Feature/Option directive WDK GDL
- constructs WDK GDL , default construct
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Adding Dependencies to the Configuration-Dependent Data


The **\*Switch**/**\*Case** directives make data depend on the parameters that are defined by using the **\*Feature**/**\*Option** directives. The construct tag of the **\*Switch** construct names one of the parameters that are defined in a **\*Feature** construct. The reference of a parameter by the construct tag of the **\*Switch** construct might precede its definition through the **\*Feature** construct.

The body of a **\*Switch** construct contains a number of **\*Case** constructs and an optional **\*Default** construct. No other child entries can appear within the **\*Switch** construct. The construct tag of the **\*Case** construct names one of the allowed values that are defined in an **\*Option** construct that correspond to the parameter that is named in the **\*Switch** construct. The construct tag is not used for the**\*Default** construct.

**\*Switch** constructs can appear as child entries within any other construct, except that a **\*Switch** construct cannot be the child of another **\*Switch** construct. The body of a **\*Case** construct can contain any GDL entries, except the **\*Case** construct cannot be the ancestor of a **\*Feature** or **\*Default** construct.

The **\*Switch**/**\*Case** directives work very similarly to the C language constructs of the same name. The contents of any **\*Case** construct (whose construct tag is named in the configuration as the current value or state of the parameter that is named by the **\*Switch** construct) are allowed to appear in the snapshot. Otherwise, the parser prevents the entries that are contained in the **\*Case** construct from appearing in the snapshot.

**Note**   Unlike the C version of **\*Switch**/**\*Case**, GDL does not need a break statement to stop execution from continuing past the end of the **\*Case** construct.

 

If the body of a**\*Case** construct is omitted (that is, **\*Case** appears as an attribute rather than a construct), the body of the next **\*Case** or **\*Default** construct will be used. This behavior is again similar to the behavior in the C language **Switch**/**Case**. If the **\*Default** construct is present, it must appear last, after all the **\*Case** entries.

If the parameter allows PICKMANY, the contents of multiple **\*Case** constructs can appear in the snapshot. This situation might lead to multiple definitions of the same construct or attribute. Such multiple definitions are handled just as if they explicitly appear in the GDL file outside of any **\*Switch**/**\*Case** construct. If several **\*Case** constructs share the same body and more than one is named in the configuration, the contents of the body will appear only once.

If none of the **\*Case** constructs are named in the configuration, the contents of the **\*Default** construct are used. If no **\*Default** construct is defined, the entire **\*Switch**/**\*Case** construct and all of its descendant entries are excluded from the snapshot.

If multiple sibling **\*Switch**/**\*Case** constructs are defined, each one is evaluated independent of the other. The merging of sibling constructs does not apply to **\*Switch**/**\*Case** constructs.

The **\*Switch** and **\*Construct** directives never appear in the snapshot, so in the snapshot, the child entries of **\*Case**construct appear as the child entries of the parent of the **\*Switch** construct.

In the following code example, a *Today* parameter is defined to take days of the week. The example shows two sibling **\*Switch**/**\*Case** constructs; both will be evaluated independently.

```
*Schedule:
{
  *Switch: Today
  {
    *Case: Saturday
    *Case: Sunday
    {
 *Eat: Breakfast, Dinner
    }
    *Case: Monday
    *Case: Wednesday
    *Case: Friday
    {
        *Eat: Lunch
    }
  }
  *Switch: Today
  {
    *Case: Sunday
    {
        *ToDo: Laundry
    }
    *Case: Saturday
    {
        *ToDo: Ballgame
    }
    *Default:
    {
        *ToDo: FixBugs
    }
    }
}
```

If the configuration specifies `Today: Saturday`, the snapshot will contain the following code.

```
*Schedule:
{
 *Eat: Breakfast, Dinner
  *ToDo: Ballgame
}
```

If the configuration specifies `Today: Wednesday`, the snapshot will contain the following code.

```
*Schedule:
{
  *Eat: Lunch
  *ToDo: FixBugs
}
```

If the configuration specifies `Today: Tuesday`, the snapshot will contain the following code.

```
*Schedule:
{
  *ToDo: FixBugs
}
```

The following code example shows two nested **\*Switch**/**\*Case** constructs.

```
*Schedule:
{
  *Switch: Today
  {
    *Case: Sunday
    {
      *Switch: Weather
      {
        *Case: Sunny
        {
            *ToDo: Garden
        }
        *Case: Cloudy
        {
            *ToDo: Laundry
        }
      }
    }
    *Case: Saturday
    {
      *ToDo: Ballgame
    }
      *Default:
      {
        *ToDo: FixBugs
      }
    }
}
```

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20Adding%20Dependencies%20to%20the%20Configuration-Dependent%20Data%20%20RELEASE:%20%289/1/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


