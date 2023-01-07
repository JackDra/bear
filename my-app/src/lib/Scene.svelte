<script lang="ts">
	import {
		AmbientLight,
		DirectionalLight,
		OrbitControls,
		PerspectiveCamera,
		Mesh
	} from '@threlte/core'
	import { MeshStandardMaterial, CircleGeometry, DoubleSide } from 'three'
	import { DEG2RAD } from 'three/src/math/MathUtils'
	import Character from '$lib/Character.svelte'
</script>

<PerspectiveCamera position={{ x: 10.6, y: 1.7, z: 2.1 }} near={0.1} far={100}>
	<OrbitControls
		maxPolarAngle={DEG2RAD * 80}
		enableRotate={true}
		enableZoom={true}
		target={{ y: 0.9 }}
	/>
</PerspectiveCamera>

<AmbientLight />
<DirectionalLight position={{ y: 10, z: 5, x: 5 }} />

<Character />

<Mesh
	receiveShadow
	rotation={{ x: -90 * (Math.PI / 180) }}
	geometry={new CircleGeometry(3, 72)}
	material={new MeshStandardMaterial({ side: DoubleSide, color: 'white' })}
/>