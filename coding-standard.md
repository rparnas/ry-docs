# Coding Standard

## Purpose
A line of code is read many more times than it is written. A consistent style makes code more readable, both for others and yourself in the future.

Coding standards need to be short enough that they can be internalized by team members. They also need to be flexible enough to allow readable code in complex situations.

## C# #
* Use tab size of 2.
* Use spaces instead of tabs.
* If groups of class members are next to each other (fields, methods, etc.) put them in alphabetical order.
* Use PascalCase for classes, fields, and property names. This means the first letter and the first letter of each word are capitalized.

````
public int FieldName;
public int PropertyName { get; set; }
````

* If you must use a backing field for a property, prefix the backing field's name with an underscore. 

````
public int PropertyName
{
  get => _PropertyName;
  set 
  { 
    _PropertyName = value; 
    SideEffects();
  }
}
int _PropertyName;

````

* Use the Allman indent style for methods. This puts the brace associated with a control statement on the next line, indented to the same level as the control statement. Statements within braces are indented to the next level.

````
public void Example()
{
  var test = 0;
}
````

* For multiple nested using directives, do not indent each directive and include braces only on the innermost level.

````
using (var a = new ThingA())
using (var b = new ThingB())
{
  a.Something(b);
}
````

* For multiple LINQ statements, use a fluent style with one statement per line like
````
var list = inputItems
  .Select(item => item.Name)
  .Where(itemName => !string.IsNullOrWhitespace(itemName))
  .ToList();
````

* Include XML tags with their contents on a single line if the contents are short.

````
<summary>A short summary.</summary>
````
