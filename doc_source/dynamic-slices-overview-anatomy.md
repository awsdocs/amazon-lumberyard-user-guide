# Anatomy of a Slice<a name="dynamic-slices-overview-anatomy"></a>

The following diagram illustrates an example slice A, which contains references to two other slices B and C\. Slice A has two instances each of B and C: 

![\[Anatomy of an example slice\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images//dynamic-slices-anatomy.png)

Each instance contains a data patch, which may be empty if no changes or overrides are present\. If the instantiation of slice B in slice A has been modified in comparison with the source asset B, the data patch contains the differences\. When slice A is instantiated again, it contains instances of slice B, but with the modifications applied\. Any nonoverridden fields propagate through the hierarchy\. If you change a property value in the slice B asset on disk, the instance of B contained in slice A will reflect that change — if the property for that instance has not already been overridden, as reflected in the instance's data patch\. 

In addition to references to other slices, slices can contain zero or more entities\. These entities are original to this slice and are not acquired through referenced slice instances\. A slice does not have to contain references to other slices\. A slice that contains only original entities \(as represented by the bottom box in the diagram\) and no references to other slices is called a *leaf slice*\. 