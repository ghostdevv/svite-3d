<script lang="ts">
    import {
        Canvas,
        Mesh,
        OrbitControls,
        PerspectiveCamera,
        DirectionalLight,
        AmbientLight,
        HemisphereLight,
    } from 'threlte';
    import { SVGLoader } from 'three/examples/jsm/loaders/SVGLoader.js';
    import sviteBolt from '$lib/svite-bolt.svg?raw';
    import { onMount } from 'svelte';
    import * as THREE from 'three';

    let sviteBoltGeometry: THREE.ExtrudeGeometry;

    onMount(() => {
        const [shape] = new SVGLoader()
            .parse(sviteBolt)
            .paths[0].toShapes(false);

        sviteBoltGeometry = new THREE.ExtrudeGeometry(shape, {
            curveSegments: 64,
            depth: 2,
            bevelEnabled: true,
            bevelOffset: 0,
            bevelSegments: 64,
            bevelSize: 1,
            bevelThickness: 2,
        });

        sviteBoltGeometry.center();
    });
</script>

<div>
    <Canvas>
        <PerspectiveCamera position={{ x: 0, y: 0, z: -100 }}>
            <OrbitControls autoRotate enableDamping />
        </PerspectiveCamera>

        <DirectionalLight
            shadow
            color={'#EDBD9C'}
            position={{ x: -20, y: 0, z: -100 }} />

        <HemisphereLight
            skyColor={0x4c8eac}
            groundColor={0xac844c}
            intensity={0.6} />

        {#if sviteBoltGeometry}
            <Mesh
                castShadow
                geometry={sviteBoltGeometry}
                position={{ x: 0, y: 0, z: 0 }}
                rotation={{ x: 0, y: 0, z: 0 }}
                material={new THREE.MeshStandardMaterial({
                    color: new THREE.Color(0xff3e00),
                    side: THREE.DoubleSide,
                })} />
        {/if}

        <Mesh
            receiveShadow
            rotation={{ x: Math.PI / 2, y: 0, z: 0 }}
            geometry={new THREE.CylinderGeometry(12, 12, 2.5, 64)}
            material={new THREE.MeshStandardMaterial({
                color: new THREE.Color(0x222222),
                side: THREE.DoubleSide,
            })} />
    </Canvas>
</div>

<style>
    div {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: #222;
    }
</style>
