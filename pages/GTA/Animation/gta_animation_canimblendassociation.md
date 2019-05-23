---
title: "CAnimBlendAssociation class"
keywords: sample homepage
sidebar: gta_sidebar
permalink: gta_animation_canimblendassociation.html
---

Animation associations are animation objects. When you press the W key on your keyboard to make your ped walk, then an instance of this class will be created for walking or running animation. If you switch animations by getting idle, running, or jumping then the current animation association will be
destroyed and replaced by a new one. 

GTA supports multiple animation associations running all at once for an entity. There are two types of animation associations:

* Primary
* Partial

The primary association is the default and main animation which is playing, it is usually one and partial animations are the ones which will play alongside of primary animations. To make an animation partial, you need to set the flag `m_bPartial` to true. 

It should be noted that animation associations are controlled by the Task System for peds. The task system has primary and secondary tasks, and it's very useful for priority.

```cpp
class CAnimBlendAssociation {
public:
    void *vtable;
    RwLLLink m_link;
    unsigned short m_nNumBlendNodes;
    unsigned short m_nAnimGroupId;
    CAnimBlendNode *m_pNodeArray;
    CAnimBlendHierarchy *m_pHierarchy;
    float m_fBlendAmount;
    float m_fBlendDelta;
    float m_fCurrentTime;
    float m_fSpeed;
    float fTimeStep;
    short m_nAnimId;
    union {
        unsigned short m_nFlags;
        struct
        {
            unsigned short m_bPlaying : 1;
            unsigned short m_bLooped : 1;
            unsigned short m_bFreezeLastFrame : 1;
            unsigned short m_bUnlockLastFrame : 1;
            unsigned short m_bPartial : 1; 
            unsigned short m_bEnableMovement : 1;
            unsigned short m_bTranslateX : 1;
            unsigned short m_bTranslateY : 1; 

            unsigned short m_bf9 : 1;
            unsigned short m_bf10 : 1;
            unsigned short m_bAddAnimBlendToTotalBlend : 1;
            unsigned short m_bf12 : 1;
            unsigned short m_bSecondaryTaskAnim : 1;
            unsigned short m_bFreezeTranslation : 1;
            unsigned short m_bBlockReferenced : 1; 
            unsigned short m_bIndestructible : 1;
        } m_nAssociationFlags;
    };
};
```

<p><code-label>vtable</code-label></p>
virtual table of the instance.

<p><code-label>m_link</code-label></p>
Animation associations use a [linked list](https://www.geeksforgeeks.org/data-structures/linked-list/) for all running animations which the entity is playing. When the destructor of this class is called for an instance, the association gets removed from the linked list and that animation stops playing for the entity. It's mainly used for peds in GTA III, VC, and SA.

<p><code-label>m_nNumBlendNodes</code-label></p>
Total nodes in the node array (`m_pNodeArray`). It is always equal to the number of bones/sequences used within the animation hierarchy.

<p><code-label>m_nAnimGroupId</code-label></p>
It is used as an index in `CAnimManager::ms_aAnimAssocGroups`.

<p><code-label>m_pNodeArray</code-label></p>
An array of blend nodes. For every animation sequence in `m_pHierarchy`, there is a blend node.

<p><code-label>m_pHierarchy</code-label></p>
The animation to be played. An animation hierarchy contains sequences which represent bones. 

<p><code-label>m_fBlendAmount</code-label></p>
The amount of blend when switching animations. It is normally set to 0.0 or 1.0.

<p><code-label>m_fBlendDelta</code-label></p>
how long the animation will mixed with the previous one. A good way to calculate it in milliseconds:

```cpp
int iBlend = 5000; // 5 seconds
float fBlendDelta = 1 / std::max((float)iBlend, 1.0f) * 1000;
```

<p><code-label>m_fCurrentTime</code-label></p>
By setting this value, you can start the animation from anywhere. If you wish to start it from the middle, then:

```cpp
float fProgress = 50.0f; // 50%
float fCurrentTime = m_pInterface->pAnimHierarchy->fTotalTime * fProgress;
```

<p><code-label>m_fSpeed</code-label></p>
Speed of the animation. Range is 0.0-2.0. If you set this to 0.5, then the animation speed is cut by half.

<p><code-label>fTimeStep</code-label></p>

<p><code-label>m_nAnimId</code-label></p>
It is used as an index in `CAnimBlendAssocGroup::m_pAssociations` to get a static association.

<p><code-label>m_nFlags</code-label></p>
If you wish to access all bits of the 2 byte flags, then use this.

<p><code-label>m_nAssociationFlags</code-label></p>

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
        <td markdown="span">m_bPlaying</td>
        <td markdown="span" ><code-label>0x01</code-label></td>
        <td markdown="span">Anim will stop playing if flag is not set.</td>
    </tr>
        <tr>
        <td markdown="span">m_bLooped</td>
        <td markdown="span" ><code-label>0x02</code-label></td>
        <td markdown="span">Anim will always restart when it completes.</td>
    </tr>
    <tr>
        <td markdown="span">m_bFreezeLastFrame</td>
        <td markdown="span" ><code-label>0x04</code-label></td>
        <td markdown="span">Anim will freeze on last frame.</td>
    </tr>
    <tr>
        <td markdown="span">_bUnlockLastFrame</td>
        <td markdown="span" ><code-label>0x08</code-label></td>
        <td markdown="span">Animation will be stuck on last frame, if not set</td>
    </tr>
    <tr>
        <td markdown="span">m_bPartial</td>
        <td markdown="span" ><code-label>0x10</code-label></td>
        <td markdown="span">Partial anims run along other anims.</td>
    </tr>
    <tr>
        <td markdown="span">m_bEnableMovement</td>
        <td markdown="span" ><code-label>0x20</code-label></td>
        <td markdown="span">Blends all playing anims together if set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bTranslateX</td>
        <td markdown="span" ><code-label>0x40</code-label></td>
        <td markdown="span">If set to false, translation for X coordinate will be ignored.</td>
    </tr>
    <tr>
        <td markdown="span">m_bTranslateY</td>
        <td markdown="span" ><code-label>0x80</code-label></td>
        <td markdown="span">Only applies if `m_bTranslateX` is set.</td>
    </tr>
    <tr>
        <td markdown="span">m_bf9</td>
        <td markdown="span" ><code-label>0x100</code-label></td>
        <td markdown="span">Unused.</td>
    </tr>
    <tr>
        <td markdown="span">m_bf10</td>
        <td markdown="span" ><code-label>0x200</code-label></td>
        <td markdown="span">Unused.</td>
    </tr>
    <tr>
        <td markdown="span">m_bAddAnimBlendToTotalBlend</td>
        <td markdown="span" ><code-label>0x400</code-label></td>
        <td markdown="span">If set to TRUE, then result: before = https://bit.ly/2WVG3N4 | after = https://bit.ly/2JXVelh</td>
    </tr>
    <tr>
        <td markdown="span">m_bf12</td>
        <td markdown="span" ><code-label>0x800</code-label></td>
        <td markdown="span">Unused.</td>
    </tr>
    <tr>
        <td markdown="span">m_bSecondaryTaskAnim</td>
        <td markdown="span" ><code-label>0x1000</code-label></td>
        <td markdown="span">Unused.</td>
    </tr>
    <tr>
        <td markdown="span">m_bFreezeTranslation</td>
        <td markdown="span" ><code-label>0x2000</code-label></td>
        <td markdown="span">Anim will play. Translation values will be ignored for anim</td>
    </tr>
    <tr>
        <td markdown="span">m_bBlockReferenced</td>
        <td markdown="span" ><code-label>0x4000</code-label></td>
        <td markdown="span">anim block can't be unloaded if it's referenced by an anim.</td>
    </tr>
    <tr>
        <td markdown="span">m_bIndestructible</td>
        <td markdown="span" ><code-label>0x8000</code-label></td>
        <td markdown="span">Anim will not be destroyed. It will be played simultaneously with other anims.</td>
    </tr>
    </tbody>
</table>

## Examples

An exmaple which illustrates how to loop through current playing animation of a ped and print their data to the console.

```cpp
CPed* pLocalPlayer = (CPed*)FindPlayerPed(-1);
if (pLocalPlayer && pLocalPlayer->m_pRwClump)
{
    auto pAnimAssociation = RpAnimBlendClumpGetFirstAssociation (pLocalPlayer->m_pRwClump);
    while (pAnimAssociation)
    {
        printf ("animation group ID: %d | animation ID: %d | partial or primary?: %s\n", 
        (int)pAnimAssociation->m_nAnimGroupId, (int)pAnimAssociation->m_nAnimId,  
        pAnimAssociation->m_nAssociationFlags.m_bPartial : "partial" ? "primary");

        pAnimAssociation = RpAnimBlendGetNextAssociation (pAnimAssociation);
    }
}
```