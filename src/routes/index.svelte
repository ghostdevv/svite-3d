<script lang="ts">
    import {
        CircleBufferGeometry,
        MeshStandardMaterial,
        BoxBufferGeometry,
        DoubleSide,
    } from 'three';
    import {
        Canvas,
        DirectionalLight,
        HemisphereLight,
        Mesh,
        OrbitControls,
        PerspectiveCamera,
    } from 'threlte';
</script>

<div>
    <Canvas>
        <PerspectiveCamera position={{ x: 10, y: 10, z: 10 }}>
            <OrbitControls autoRotate />
        </PerspectiveCamera>

        <DirectionalLight
            shadow
            color={'white'}
            position={{ x: -15, y: 45, z: 20 }} />
        <HemisphereLight
            skyColor={'white'}
            groundColor={'#ac844c'}
            intensity={0.4} />

        <Mesh
            castShadow
            geometry={new BoxBufferGeometry(1, 1, 1)}
            material={new MeshStandardMaterial({ color: '#ff3e00' })} />
    </Canvas>
</div>

<style>
    div {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
</style>
