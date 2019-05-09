---
title: "CPhysical class"
keywords: sample homepage
sidebar: gta_sidebar
permalink: gta_entity_cphysical.html
---

This class inherits from CEntity. As the name describes, it has functions for applying physics to entities.

```cpp
class CPhysical : public CEntity {
public:
    int field_38;
    unsigned int m_nLastCollisionTime;
    struct {
        unsigned int b01 : 1;
        unsigned int bApplyGravity : 1;
        unsigned int bDisableCollisionForce : 1;
        unsigned int bCollidable : 1;
        unsigned int bDisableTurnForce : 1;
        unsigned int bDisableMoveForce : 1;
        unsigned int bInfiniteMass : 1;
        unsigned int bDisableZ : 1;

        unsigned int bSubmergedInWater : 1;
        unsigned int bOnSolidSurface : 1;
        unsigned int bBroken : 1;
        unsigned int b12 : 1;
        unsigned int b13 : 1;
        unsigned int bDontApplySpeed : 1;
        unsigned int b15 : 1;
        unsigned int b16 : 1;

        unsigned int b17 : 1;
        unsigned int b18 : 1; 
        unsigned int bBulletProof : 1;
        unsigned int bFireProof : 1;
        unsigned int bCollisionProof : 1;
        unsigned int bMeeleProof : 1;
        unsigned int bInvulnerable : 1;
        unsigned int bExplosionProof : 1;

        unsigned int b25 : 1;
        unsigned int bAttachedToEntity : 1;
        unsigned int b27 : 1;
        unsigned int bTouchingWater : 1;
        unsigned int bCanBeCollidedWith : 1;
        unsigned int bDestroyed : 1;
        unsigned int b31 : 1;
        unsigned int b32 : 1;
    } m_nPhysicalFlags;
    CVector          m_vecMoveSpeed;
    CVector          m_vecTurnSpeed;
    CVector          m_vecFrictionMoveSpeed;
    CVector          m_vecFrictionTurnSpeed;
    CVector          m_vecForce;
    CVector          m_vecTorque;
    float            m_fMass;
    float            m_fTurnMass;
    float            m_fVelocityFrequency;
    float            m_fAirResistance;
    float            m_fElasticity;
    float            m_fBuoyancyConstant;
    CVector          m_vecCentreOfMass;
    void            *m_pCollisionList;
    void            *m_pMovingList;
    char field_B8;
    unsigned char    m_nNumEntitiesCollided;
    unsigned char    m_nContactSurface;
    char field_BB;
    CEntity         *m_apCollidedEntities[6];
    float            m_fMovingSpeed;
    float            m_fDamageIntensity;
    CEntity         *m_pDamageEntity;
    CVector          m_vecLastCollisionImpactVelocity;
    CVector          m_vecLastCollisionPosn;
    unsigned short   m_nPieceType;
    short field_FA;
    class CPhysical *m_pAttachedTo;
    CVector          m_vecAttachOffset;
    CVector          m_vecAttachedEntityPosn;
    CQuaternion      m_qAttachedEntityRotation;
    CEntity         *m_pEntityIgnoredCollision;
    float            m_fContactSurfaceBrightness;
    float            m_fDynamicLighting;
    CRealTimeShadow *m_pShadowData;
```

<p><code-label>field_38</code-label></p>
Unknown field of 4 bytes.

<p><code-label>m_nLastCollisionTime</code-label></p>
The last time when collision was processed. If you want to know the total time passed since last collision processing, then do this:

```cpp
DWORD timePassedSinceLastCollisionInMs = CTimer::m_snTimeInMilliseconds - pVehicle->m_dwLastCollisionTime;
```

<p><code-label>m_nPhysicalFlags</code-label></p>

<table>
    <colgroup>
        <col width="30%" />
        <col width="10%" />
        <col width="60%" />
    </colgroup>
    <thead>
        <tr class="header">
            <th>Flag</th>
            <th>Value</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td markdown="span">b01</td>
        <td markdown="span" ><code-label>0x01</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
        <tr>
        <td markdown="span">bApplyGravity</td>
        <td markdown="span" ><code-label>0x02</code-label></td>
        <td markdown="span">If this flag is not set, then `CPhysical::ApplyGravity` function will not execute for this entity.</td>
    </tr>
    <tr>
        <td markdown="span">bDisableCollisionForce</td>
        <td markdown="span" ><code-label>0x04</code-label></td>
        <td markdown="span">If this flag is set, then collision force from other entities will not affect this one.</td>
    </tr>
    <tr>
        <td markdown="span">bCollidable</td>
        <td markdown="span" ><code-label>0x08</code-label></td>
        <td markdown="span">This flag is set, this entity will be able to collide with others.</td>
    </tr>
    <tr>
        <td markdown="span">bDisableTurnForce</td>
        <td markdown="span" ><code-label>0x10</code-label></td>
        <td markdown="span">If this flag is set, then `CPhysical::ApplyTurnForce` function will not execute for this entity.</td>
    </tr>
    <tr>
        <td markdown="span">bDisableMoveForce</td>
        <td markdown="span" ><code-label>0x20</code-label></td>
        <td markdown="span">If this flag is set, then `CPhysical::ApplyMoveForce` function will not execute for this entity.</td>
    </tr>
    <tr>
        <td markdown="span">bInfiniteMass</td>
        <td markdown="span" ><code-label>0x40</code-label></td>
        <td markdown="span">If set, force will not work on this entity?</td>
    </tr>
    <tr>
        <td markdown="span">bDisableZ</td>
        <td markdown="span" ><code-label>0x80</code-label></td>
        <td markdown="span">If set, Z value (up and down) will remain unchanged during collision.</td>
    </tr>
    <tr>
        <td markdown="span">bSubmergedInWater</td>
        <td markdown="span" ><code-label>0x100</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity is completely under water.</td>
    </tr>
    <tr>
        <td markdown="span">bOnSolidSurface</td>
        <td markdown="span" ><code-label>0x200</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity is on a solid surface or not.</td>
    </tr>
    <tr>
        <td markdown="span">bBroken</td>
        <td markdown="span" ><code-label>0x400</code-label></td>
        <td markdown="span">This flag is used to determine that the entity is broken or not.</td>
    </tr>
    <tr>
        <td markdown="span">b12</td>
        <td markdown="span" ><code-label>0x800</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">b13</td>
        <td markdown="span" ><code-label>0x1000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">bDontApplySpeed</td>
        <td markdown="span" ><code-label>0x2000</code-label></td>
        <td markdown="span"></td>
    </tr>
    <tr>
        <td markdown="span">b15</td>
        <td markdown="span" ><code-label>0x4000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">b16</td>
        <td markdown="span" ><code-label>0x8000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">b17</td>
        <td markdown="span" ><code-label>0x10000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">b18</td>
        <td markdown="span" ><code-label>0x20000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">bBulletProof</td>
        <td markdown="span" ><code-label>0x40000</code-label></td>
        <td markdown="span">If set, the entity will not receive any damage from bullets.</td>
    </tr>
    <tr>
        <td markdown="span">bFireProof</td>
        <td markdown="span" ><code-label>0x80000</code-label></td>
        <td markdown="span">If set, the entity will not receive any damage from fire.</td>
    </tr>
    <tr>
        <td markdown="span">bCollisionProof</td>
        <td markdown="span" ><code-label>0x100000</code-label></td>
        <td markdown="span">If set, the entity will not receive any damage from collision.</td>
    </tr>
    <tr>
        <td markdown="span">bMeeleProof </td>
        <td markdown="span" ><code-label>0x200000</code-label></td>
        <td markdown="span">If set, the entity will not receive any damage from melee attacks.</td>
    </tr>
    <tr>
        <td markdown="span">bInvulnerable</td>
        <td markdown="span" ><code-label>0x400000</code-label></td>
        <td markdown="span"></td>
    </tr>
    <tr>
        <td markdown="span">bExplosionProof</td>
        <td markdown="span" ><code-label>0x800000</code-label></td>
        <td markdown="span">If set, the entity will not receive any damage from explosions.</td>
    </tr>
    <tr>
        <td markdown="span">b25</td>
        <td markdown="span" ><code-label>0x100000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">bAttachedToEntity</td>
        <td markdown="span" ><code-label>0x2000000</code-label></td>
        <td markdown="span">This flag is used to determine that the entity is attached to other entities or not.</td>
    </tr>
    <tr>
        <td markdown="span">b27</td>
        <td markdown="span" ><code-label>0x4000000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">bTouchingWater</td>
        <td markdown="span" ><code-label>0x8000000</code-label></td>
        <td markdown="span">This flag is used to determine that the entity is touching water or not.</td>
    </tr>
    <tr>
        <td markdown="span">bCanBeCollidedWith</td>
        <td markdown="span" ><code-label>0x1000000</code-label></td>
        <td markdown="span"></td>
    </tr>
    <tr>
        <td markdown="span">bDestroyed</td>
        <td markdown="span" ><code-label>0x20000000</code-label></td>
        <td markdown="span">It's mainly used for vehicles to check if they have exploded or not.</td>
    </tr>
    <tr>
        <td markdown="span">b31</td>
        <td markdown="span" ><code-label>0x40000000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    <tr>
        <td markdown="span">b33</td>
        <td markdown="span" ><code-label>0x80000000</code-label></td>
        <td markdown="span">Unknown bit.</td>
    </tr>
    </tbody>
</table>

<p><code-label>m_vecMoveSpeed</code-label></p>
Moving speed of the entity.

<p><code-label>m_vecTurnSpeed</code-label></p>
Turning speed of the entity.

<p><code-label>m_vecFrictionMoveSpeed</code-label></p>
Moving speed of the entity with friction applied.

<p><code-label>m_vecFrictionTurnSpeed</code-label></p>
Turning speed of the entity with friction applied.

<p><code-label>m_vecForce</code-label></p>
Force of the entity.

<p><code-label>m_vecTorque</code-label></p>
Force required to rotate the entity about its axis.

<p><code-label>m_fMass</code-label></p>
Mass of the entity.

<p><code-label>m_fTurnMass</code-label></p>
Turning mass of the entity.

<p><code-label>m_fVelocityFrequency</code-label></p>

<p><code-label>m_fAirResistance</code-label></p>
The higher the value, the greater the resistance will be.

<p><code-label>m_fElasticity</code-label></p>
Elasticity of the entity.

<p><code-label>m_fBuoyancyConstant</code-label></p>
Used when the entity in underwater.

<p><code-label>m_vecCentreOfMass</code-label></p>
Centre of mass of the entity.

<p><code-label>m_pCollisionList</code-label></p>
Pointer to a [doubly linked list](https://www.geeksforgeeks.org/doubly-linked-list/) of collision entites (CPtrNodeDoubleLink)?

<p><code-label>m_pMovingList</code-label></p>
Pointer to a [doubly linked list](https://www.geeksforgeeks.org/doubly-linked-list/) of moving entites (CPtrNodeDoubleLink).

<p><code-label>m_fMovingSpeed</code-label></p>
Moving speed of the entity in current direction.

<p><code-label>m_fDamageIntensity</code-label></p>
Damage intensity of the entity.

<p><code-label>m_pDamageEntity</code-label></p>
Pointer to entity that is inflicting damage upon this entity.

<p><code-label>m_vecLastCollisionImpactVelocity</code-label></p>
U

<p><code-label>m_vecLastCollisionPosn</code-label></p>
U

<p><code-label>m_nPieceType</code-label></p>
Uses eCollisionComponents.

```cpp
COLLISION_DEFAULT  = 0
COLLISION_BONNET  = 1
COLLISION_BOOT   = 2
COLLISION_BUMP_FRONT  = 3
COLLISION_BUMP_REAR  = 4
COLLISION_DOOR_LF  = 5
COLLISION_DOOR_RF  = 6
COLLISION_DOOR_LR  = 7
COLLISION_DOOR_RR  = 8
COLLISION_WING_LF  = 9
COLLISION_WING_RF  = 0Ah
COLLISION_WING_LR  = 0Bh
COLLISION_WING_RR  = 0Ch
COLLISION_WINDSCREEN  = 13h
```

<p><code-label>field_FA</code-label></p>
Unknown field of 2 bytes.

<p><code-label>m_pAttachedTo</code-label></p>
Pointer to entity that you want to attach to.

<p><code-label>m_vecAttachOffset</code-label></p>
Attach offsets from the target entity position.

<p><code-label>m_vecAttachedEntityPosn</code-label></p>
If m_vecAttachOffset is set, then this vector describes the position of this entity. It might also mean the last position where the entity was attached?

<p><code-label>m_qAttachedEntityRotation</code-label></p>
If m_vecAttachOffset is set, this quartenion describes rotation for this entity and m_vecAttachOffset is used as axis.

<p><code-label>m_pEntityIgnoredCollision</code-label></p>
If set, collision will be ignored with the specific entity. This is normally set to the entity that it's attached to.

<p><code-label>m_fContactSurfaceBrightness</code-label></p>

<p><code-label>m_fDynamicLighting</code-label></p>
This value is mainly used in `CPointLights::GenerateLightsAffectingObject`.

<p><code-label>m_pShadowData</code-label></p>
Shadow data of the entity.
