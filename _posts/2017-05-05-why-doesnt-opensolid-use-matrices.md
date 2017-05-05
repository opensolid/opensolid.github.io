---
categories: posts
title: Why Doesn't OpenSolid Use Matrices?
tags: frame transformation matrix
---

# A section

## A sub-section

  - A bullet
  - Another bullet

Some code:

{% highlight elm %}
module OpenSolid.LinearAlgebra.Point3d
    exposing
        ( toVec3
        , fromVec3
        , transformBy
        )

import OpenSolid.Geometry.Types exposing (..)
import OpenSolid.Point3d as Point3d
import Math.Vector3 exposing (Vec3)
import Math.Matrix4 exposing (Mat4)


toVec3 : Point3d -> Vec3
toVec3 point =
    Math.Vector3.fromTuple (Point3d.coordinates point)


fromVec3 : Vec3 -> Point3d
fromVec3 vec =
    Point3d (Math.Vector3.toTuple vec)


transformBy : Mat4 -> Point3d -> Point3d
transformBy matrix point =
    let
        { m11, m12, m13, m14, m21, m22, m23, m24, m31, m32, m33, m34, m41, m42, m43, m44 } =
            Math.Matrix4.toRecord matrix

        ( x, y, z ) =
            Point3d.coordinates point
    in
        Point3d
            ( m11 * x + m12 * y + m13 * z + m14
            , m21 * x + m22 * y + m23 * z + m24
            , m31 * x + m32 * y + m33 * z + m34
            )
{% endhighlight %}