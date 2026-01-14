<script lang="ts">
  import { T } from '@threlte/core'
  import { BufferGeometry, BufferAttribute, Sphere, Vector3 } from 'three'

  const fullscreenTriGeometry = (() => {
    const geometry = new BufferGeometry()

    const positions = new Float32Array([-1.0, -1.0, 3.0, -1.0, -1.0, 3.0])

    const uvs = new Float32Array([0.0, 0.0, 2.0, 0.0, 0.0, 2.0])

    geometry.setAttribute('position', new BufferAttribute(positions, 2))
    geometry.setAttribute('uv', new BufferAttribute(uvs, 2))

    //Prevents Error: THREE.BufferGeometry.computeBoundingSphere(): Computed radius is NaN.
    geometry.boundingSphere = new Sphere(new Vector3(), Infinity)

    return geometry
  })()

  let { children, ...meshProps } = $props()
</script>

<T.Mesh geometry={fullscreenTriGeometry} frustumCulled={false} {...meshProps}>
  {@render children?.()}
</T.Mesh>
