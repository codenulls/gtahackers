---
title: "CEntity class"
keywords: sample homepage
sidebar: gta_sidebar
permalink: gta_entity_centity.html
---

An instance of this class can be a ped, building, vehicle, or dynamic object (created by scripts). 

```cpp
class  CEntity : public CPlaceable {
public:
    union {
        struct RwObject *m_pRwObject;
        struct RpClump *m_pRwClump;
        struct RpAtomic *m_pRwAtomic;
    } RenderwareObject;
    union {
        struct {
            unsigned int m_bUsesCollision : 1;          
            unsigned int m_bCollisionProcessed : 1;  
            unsigned int m_bIsStatic : 1;              
            unsigned int m_bHasContacted : 1;         
            unsigned int m_bIsStuck : 1;            
            unsigned int m_bIsInSafePosition : 1;       
            unsigned int m_bWasPostponed : 1;  
            unsigned int m_bIsVisible : 1;  

            unsigned int m_bIsBIGBuilding : 1;  
            unsigned int m_bRenderDamaged : 1;  
            unsigned int m_bStreamingDontDelete : 1;
            unsigned int m_bRemoveFromWorld : 1;   
            unsigned int m_bHasHitWall : 1;     
            unsigned int m_bImBeingRendered : 1;
            unsigned int m_bDrawLast : 1;   
            unsigned int m_bDistanceFade : 1;  

            unsigned int m_bDontCastShadowsOn : 1;  
            unsigned int m_bOffscreen : 1;    
            unsigned int m_bIsStaticWaitingForCollision : 1;
            unsigned int m_bDontStream : 1;  
            unsigned int m_bUnderwater : 1;    
            unsigned int m_bHasPreRenderEffects : 1;
            unsigned int m_bIsTempBuilding : 1;  
            unsigned int m_bDontUpdateHierarchy : 1;

            unsigned int m_bHasRoadsignText : 1;     
            unsigned int m_bDisplayedSuperLowLOD : 1;
            unsigned int m_bIsProcObject : 1;           
            unsigned int m_bBackfaceCulled : 1; 
            unsigned int m_bLightObject : 1; 
            unsigned int m_bUnimportantStream : 1;     
            unsigned int m_bTunnel : 1;   
            unsigned int m_bTunnelTransition : 1;   
        };
        unsigned int m_nFlags;
    } Flags;

    unsigned short m_nRandomSeed;
    unsigned short m_nModelIndex;
    CReference *m_pReferences;
    void *m_pStreamingLink;
    short m_nScanCode;
    char m_nIplIndex;
    unsigned char m_nAreaCode;
    union {
        int m_nLodIndex;
        CEntity *m_pLod;
    } LOD;
    unsigned char m_nNumLodChildren;
    unsigned char m_nNumLodChildrenRendered;
    unsigned char m_nType : 3;
    unsigned char m_nStatus : 5;
};
```


<p><code-label>RenderwareObject</code-label></p>
**RenderwareObject** describes a union with three different types.

<p><code-label>RenderwareObject.m_pRwObject</code-label></p>
RenderWare object of the entity.

<p><code-label>RenderwareObject.m_pRwClump</code-label></p>
RenderWare clump of the entity.

<p><code-label>RenderwareObject.m_pRwAtomic</code-label></p>
RenderWare atomic of the entity.

<p><code-label>Flags</code-label></p>

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
        <td markdown="span">m_bUsesCollision</td>
        <td markdown="span" ><code-label>0x01</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity uses collision.</td>
    </tr>
        <tr>
        <td markdown="span">m_bCollisionProcessed</td>
        <td markdown="span" ><code-label>0x02</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity has been processed by a ProcessEntityCollision function.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsStatic</td>
        <td markdown="span" ><code-label>0x04</code-label></td>
        <td markdown="span">This flag is used to indicate whether the entity is static.</td>
    </tr>
    <tr>
        <td markdown="span">m_bHasContacted</td>
        <td markdown="span" ><code-label>0x08</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity has processed some contact forces.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsStuck</td>
        <td markdown="span" ><code-label>0x10</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity is stuck.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsInSafePosition</td>
        <td markdown="span" ><code-label>0x20</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity is in a collision free safe position.</td>
    </tr>
    <tr>
        <td markdown="span">m_bWasPostponed</td>
        <td markdown="span" ><code-label>0x40</code-label></td>
        <td markdown="span">This flag is used to determine whether the control processing of entity was postponed (ProcessControl functions).</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsVisible</td>
        <td markdown="span" ><code-label>0x80</code-label></td>
        <td markdown="span">This flag is set when the entity is visible.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsBIGBuilding</td>
        <td markdown="span" ><code-label>0x100</code-label></td>
        <td markdown="span">This flag is set when the entity is a big building.</td>
    </tr>
    <tr>
        <td markdown="span">m_bRenderDamaged</td>
        <td markdown="span" ><code-label>0x200</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity has processed some contact forces.</td>
    </tr>
    <tr>
        <td markdown="span">m_bStreamingDontDelete</td>
        <td markdown="span" ><code-label>0x400</code-label></td>
        <td markdown="span">This flag is used to determine that the entity is not allowed to be deleted by streaming (CStreaming functions).</td>
    </tr>
    <tr>
        <td markdown="span">m_bRemoveFromWorld</td>
        <td markdown="span" ><code-label>0x800</code-label></td>
        <td markdown="span">This flag is used to determine that the entity should be removed when it's processed next time.</td>
    </tr>
    <tr>
        <td markdown="span">m_bHasHitWall</td>
        <td markdown="span" ><code-label>0x1000</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity has collided with a building (changes subsequent collisions).</td>
    </tr>
    <tr>
        <td markdown="span">m_bImBeingRendered</td>
        <td markdown="span" ><code-label>0x2000</code-label></td>
        <td markdown="span">This flag is used to determine that the entity should not be deleted because it's being rendered.</td>
    </tr>
    <tr>
        <td markdown="span">m_bDrawLast</td>
        <td markdown="span" ><code-label>0x4000</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity should be drawn last in rendering order.</td>
    </tr>
    <tr>
        <td markdown="span">m_bDistanceFade</td>
        <td markdown="span" ><code-label>0x8000</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity should fade because it is far away.</td>
    </tr>
    <tr>
        <td markdown="span">m_bDontCastShadowsOn</td>
        <td markdown="span" ><code-label>0x10000</code-label></td>
        <td markdown="span">Shadows are not casted on the object when this flag is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bOffscreen</td>
        <td markdown="span" ><code-label>0x20000</code-label></td>
        <td markdown="span">.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsStaticWaitingForCollision</td>
        <td markdown="span" ><code-label>0x40000</code-label></td>
        <td markdown="span">This flag is used by script created entities - they are static until the collision is loaded below them.</td>
    </tr>
    <tr>
        <td markdown="span">m_bDontStream</td>
        <td markdown="span" ><code-label>0x80000</code-label></td>
        <td markdown="span">The GTA streamer will not stream the entity when this flag is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bUnderwater</td>
        <td markdown="span" ><code-label>0x100000</code-label></td>
        <td markdown="span">This flag is used to determine that the entity is underwater change drawing order.</td>
    </tr>
    <tr>
        <td markdown="span">m_bHasPreRenderEffects</td>
        <td markdown="span" ><code-label>0x200000</code-label></td>
        <td markdown="span">This flag indicates that the entity has prerender effects attached to it.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsTempBuilding</td>
        <td markdown="span" ><code-label>0x400000</code-label></td>
        <td markdown="span">This flag indicates that the entity is a temporary building (i.e. can be created and deleted more than once).</td>
    </tr>
    <tr>
        <td markdown="span">m_bDontUpdateHierarchy</td>
        <td markdown="span" ><code-label>0x800000</code-label></td>
        <td markdown="span">The animation hierarchy is not updated for the frame when this flag is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bHasRoadsignText</td>
        <td markdown="span" ><code-label>0x100000</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity is a roadsign and has some 2deffect text stuff to be rendered.</td>
    </tr>
    <tr>
        <td markdown="span">m_bDisplayedSuperLowLOD</td>
        <td markdown="span" ><code-label>0x2000000</code-label></td>
        <td markdown="span">A very low detailed (less vertices) version of the entity is rendered when this flag is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIsProcObject</td>
        <td markdown="span" ><code-label>0x4000000</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity has been generate by procedural object generator.</td>
    </tr>
    <tr>
        <td markdown="span">m_bBackfaceCulled</td>
        <td markdown="span" ><code-label>0x8000000</code-label></td>
        <td markdown="span">The object will be affected by Back-face culling when the flag is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bLightObject</td>
        <td markdown="span" ><code-label>0x1000000</code-label></td>
        <td markdown="span">The object is light with directional lights when this flag is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bUnimportantStream</td>
        <td markdown="span" ><code-label>0x20000000</code-label></td>
        <td markdown="span">.</td>
    </tr>
    <tr>
        <td markdown="span">m_bTunnel</td>
        <td markdown="span" ><code-label>0x40000000</code-label></td>
        <td markdown="span">This flag is used to determine whether the entity is part of a tunnel or not.</td>
    </tr>
    <tr>
        <td markdown="span">m_bTunnelTransition</td>
        <td markdown="span" ><code-label>0x80000000</code-label></td>
        <td markdown="span">The model is rendered from within and outside of the tunnel when set.</td>
    </tr>
    </tbody>
</table>

<p><code-label>Flags.m_nFlags</code-label></p>
Use this to access or set flags if you wish to as it contains all 32 bits (4 bytes).

<p><code-label>m_nRandomSeed</code-label></p>
Self-explanatory. Go to [this link](https://stackoverflow.com/questions/22639587/random-seed-what-does-it-do) for more info.

<p><code-label>m_nModelIndex</code-label></p>
Refers to the ID of the model. It is usually used in `CModelInfo::ms_modelInfoPtrs` which gives you a pointer to `CBaseModelInfo` instance of the entity model.

<p><code-label>m_pReferences</code-label></p>
Entities that are interacting with this entity in one way or the other.  

<p><code-label>m_pStreamingLink</code-label></p>
<p><code-label>m_nScanCode</code-label></p>
It is used to avoid duplicate queries in sector list processing. Whenever the game is scanning for entities that are present in world, this member is compared with `CWorld::ms_nCurrentScanCode`, and if both values are not equal, then the value of `CWorld::ms_nCurrentScanCode` is copied to this member.

<p><code-label>m_nIplIndex</code-label></p>
It is used to determine which IPL the entity belongs to. This member might be set by any of these three functions:
<ul>
  <li>CIplStore::LoadIpl</li>
  <li>CIplStore::LoadIplBoundingBox</li>
  <li>CFileLoader::LoadObjectInstance</li>
</ul> 

<p><code-label>m_nAreaCode</code-label></p>

Current [interior](https://wiki.multitheftauto.com/wiki/Interior) of the entity. 

<p><code-label>LOD</code-label></p>
**LOD** describes a union with two different types.

<p><code-label>LOD.m_nLodIndex</code-label></p>
If the entity has no LOD, then this is set to -1. 

<p><code-label>LOD.m_pLod</code-label></p>
If the entity contains a LOD, then this will point to that LOD entity, otherwise it is set to nullptr.

<p><code-label>m_nNumLodChildren</code-label></p>
Number of high LODs for the entity. It is normally used to check whether an entity has a LOD or not, if the LOD exists, then the value of this member is greater than zero.

<p><code-label>m_nNumLodChildrenRendered</code-label></p>
If alpha == 255, then `CRenderer::SetupMapEntityVisibility` will increment the value of this member when called.

<p><code-label>m_nType</code-label></p>
See eEntityType.

<p><code-label>m_nStatus</code-label></p>
See eEntityStatus.