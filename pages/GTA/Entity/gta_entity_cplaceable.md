---
title: "CPlaceable class"
keywords: sample homepage
sidebar: gta_sidebar
permalink: gta_entity_cplaceable.html
---

This class is used by CEntity. Whenever you wish to change the position or rotation of an entity, simply modify the position vector or angle in m_placement, respectively, and then update the matrix.

```cpp
class CPlaceable {
public:
    CSimpleTransform m_placement;
    CMatrixLink *m_matrix;
};
```

<p><code-label>m_placement</code-label></p>
X, Y, and Z position values, along with a rotation angle. 

<p><code-label>m_matrix</code-label></p>
Contains same values as m_placement but in the form of a matrix.

## Examples

An example which illustrates how to properly change the position and rotation of an object.

```cpp
// Assuming pObject is a pointer to a CObect entity
CVector newPosition (100.0f, 150.0f, 5.f);

// set the new rotation
pObject->m_placement.SetRotate(0.0, 0.0, 0.0);

// set the new position
pObject->m_placement.pos = newPosition;

// after setting the position and rotation, we need to update 
// the matrix by calling UpdateRW
pObject->m_placement.UpdateRW();
pObject->UpdateRwFrame();
```