<script>
  import { tweened } from 'svelte/motion';
  import { cubicInOut } from 'svelte/easing';
  import { generateRingSteps } from '$lib/utils';
  import { 
    T, 
    useFrame, 
    OrbitControls, 
    TransformableObject 
  } from '@threlte/core';
  import { Grid } from '@threlte/extras';
  
  export let index
  export let offset
  export let progress

  let r = 0;
  let meshRef;
  const cameraPosition = tweened(null, { duration: 1000, easing: cubicInOut })

  useFrame((_, delta) => {
    r += 0.5 * delta;
  })

  // Predefined locations for camera movement
  const cameraSteps = [
    ...generateRingSteps(10, 20)
  ]

  // Update camera position based on scroller index
  $: cameraPosition.set(cameraSteps[index] ?? cameraSteps[0])
</script>

<T.PerspectiveCamera 
    makeDefault
    position.x={$cameraPosition.x}
    position.y={$cameraPosition.y}
    position.z={$cameraPosition.z}
    fov={55}
    let:ref={camRef}
  >
    <TransformableObject 
      object={camRef} 
      lookAt={meshRef} 
    />
</T.PerspectiveCamera>

<T.HemisphereLight color="#00ff00" groundColor="#0000ff" intensity={0.5}/>

<T.Mesh rotation.x={r} rotation.y={r} bind:ref={meshRef}>
  <T.IcosahedronGeometry />
  <T.MeshStandardMaterial color="#ffffff" />
</T.Mesh>

<Grid 
  infiniteGrid 
  fadeDistance={50} 
  cellColor="#ffffff"
  sectionColor="#ff0500"
/>