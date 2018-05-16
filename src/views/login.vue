<template>
    <div>
        <div id="canvascontainer" ref='can'></div>
        <div id="login" class="login">
            <img class="title" src="https://raw.githubusercontent.com/Selegant/solution-vue/master/static/image/title.png"/>
            <div class="login-con">
                <Card :bordered="false">
                    <p slot="title">
                        <Icon type="log-in"></Icon>
                        欢迎登录
                    </p>
                    <div class="form-con">
                        <Form ref="loginForm" :model="form" :rules="rules">
                            <FormItem prop="userName">
                                <Input v-model="form.userName" placeholder="请输入用户名"/><span slot="prepend"><Icon
                                :size="16"
                                type="person"></Icon></span>
                            </FormItem>
                            <FormItem prop="password">
                                <Input type="password" v-model="form.password" placeholder="请输入密码"/><span
                                slot="prepend"><Icon
                                :size="14" type="locked"></Icon></span>
                            </FormItem>
                            <FormItem>
                                <Button type="primary" class="button">登录</Button>
                                <Button type="primary" class="button">注册</Button>
                            </FormItem>
                        </Form>
                    </div>
                </Card>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                form: {
                    userName: '',
                    password: ''
                },
                rules: {
                    userName: [
                        {required: true, message: '账号不能为空', trigger: 'blur'}
                    ],
                    password: [
                        {required: true, message: '密码不能为空', trigger: 'blur'}
                    ]
                }
            }
        },
        mounted() {
            container = document.createElement('div');
            this.$refs.can.appendChild(container);
            camera = new THREE.PerspectiveCamera(100, window.innerWidth / window.innerHeight, 1, 10000);
            camera.position.z = 1000;
            scene = new THREE.Scene();
            particles = new Array();
            var PI2 = Math.PI * 2;
            var material = new THREE.ParticleCanvasMaterial({
                color: 0x0078de,
                program: function (context) {
                    context.beginPath();
                    context.arc(0, 0, 1, 0, PI2, true);
                    context.fill();
                }
            });
            var i = 0;
            for (var ix = 0; ix < AMOUNTX; ix++) {
                for (var iy = 0; iy < AMOUNTY; iy++) {
                    particle = particles[i++] = new THREE.Particle(material);
                    particle.position.x = ix * SEPARATION - ((AMOUNTX * SEPARATION) / 2);
                    particle.position.z = iy * SEPARATION - ((AMOUNTY * SEPARATION) / 2);
                    scene.add(particle);
                }
            }
            renderer = new THREE.CanvasRenderer();
            renderer.setSize(window.innerWidth, window.innerHeight);
            container.appendChild(renderer.domElement);
            document.addEventListener('mousemove', onDocumentMouseMove, false);
            window.addEventListener('resize', onWindowResize, false);
            animate();
        }
    }

    var SEPARATION = 100, AMOUNTX = 50, AMOUNTY = 50;
    var container;
    var camera, scene, renderer;
    var particles, particle, count = 0;
    var mouseX = 0, mouseY = -300;
    var windowHalfX = window.innerWidth / 2;
    var windowHalfY = window.innerHeight / 2;
    // animate();
    function init() {

    }

    function onWindowResize() {
        windowHalfX = window.innerWidth / 2;
        windowHalfY = window.innerHeight / 2;
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    }

    //

    function onDocumentMouseMove(event) {
        mouseX = event.clientX - windowHalfX;
        // mouseY = event.clientY - windowHalfY;
    }

    function onDocumentTouchStart(event) {
        if (event.touches.length === 1) {
            event.preventDefault();
            mouseX = event.touches[0].pageX - windowHalfX;
            mouseY = event.touches[0].pageY - windowHalfY;
        }
    }

    function onDocumentTouchMove(event) {
        if (event.touches.length === 1) {
            event.preventDefault();
            mouseX = event.touches[0].pageX - windowHalfX;
            mouseY = event.touches[0].pageY - windowHalfY;
        }
    }

    //

    function animate() {
        requestAnimationFrame(animate);
        render();
    }

    function render() {
        camera.position.x += (mouseX - camera.position.x) * 0.05;
        camera.position.y += (-mouseY - camera.position.y) * 0.05;
        camera.lookAt(scene.position);
        var i = 0;
        for (var ix = 0; ix < AMOUNTX; ix++) {
            for (var iy = 0; iy < AMOUNTY; iy++) {
                particle = particles[i++];
                particle.position.y = (Math.sin((ix + count) * 0.3) * 50) + (Math.sin((iy + count) * 0.5) * 50);
                particle.scale.x = particle.scale.y = (Math.sin((ix + count) * 0.3) + 1) * 2 + (Math.sin((iy + count) * 0.5) + 1) * 2;
            }
        }
        renderer.render(scene, camera);
        count += 0.1;
    }
</script>

<style scoped>
    #canvascontainer {
        position: absolute;
        top: 150px;
    }
    .title{
        margin-bottom: 10%;
        margin-left: -52%;
    }
    .login {
        width: 20%;
        height: 10%;
        position: relative;
        margin: 10% auto;
    }
    .form-con{
        padding: 10px 0 0;
    }
    .login-tip{
        font-size: 10px;
        text-align: center;
        color: #c3c3c3;
    }
    .button{
        margin: 2%;
        width: 45%;
    }
</style>
