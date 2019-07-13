<template>
    <header class="page-header">
        <div class="page-header__content">
            <div class="page-header__logo" @click="onLogoClick">
                <Logo />
            </div>
            <span class="toogle">
                <a href="#" @click="onMenuClick">☰</a>
            </span>
            <nav v-bind:class= "classObject" >
                <div id="menu">
                    <ul>
                        <li><a href="#">about us</a></li>
                        <li><a href="#">contact</a></li>
                        <li><a href="#">our history</a></li>
                        <li><a href="#">our team</a></li>
                    </ul>
                </div>
            </nav>
        </div>
    </header>
</template>
<script>
    import Logo from '@img/fitatu.svg';

    export default {
        data() {
            return{
                classObject: {
                    'visible': false,
                    'hidden': true,
                }                
            }
        },

        methods: {
            onMenuClick(){
                        this.classObject.visible = !this.classObject.visible;
                        this.classObject.hidden = !this.classObject.hidden
            }
        },
        props: {
            onLogoClick: {
                type: Function,
                default: () => {},
            },
        },
        components: {
            Logo,
        },
    };
</script>
<style lang="scss" scoped>

    $break-small: 960px;

    .page-header {
        height: 60px;
        

        &__content {
            display: flex;
            align-items: center;
            justify-content: center;

            position: fixed;
            z-index: 11;
            height: inherit;
            width: 100%;
            background-color: #fff;
            box-shadow: 0 0 15px #ced0d0;

            nav{
                position: absolute;
                right: 2%;
                li{
                    display: inline-block;
                    font-weight: 800;
                    padding: 0 0 0 2rem;
                    a{
                        text-decoration:none;
                        color: black;
                    }
                }
            }

            .toogle{
                position: absolute;
                right: 2%;
                a{
                    text-decoration: none;
                    color: black;
                    font-weight: 800;
                    font-size: 1.3em;
                }  
            }

            @media(min-width: $break-small){
                .toogle{
                    display: none;
                }
            }

            @media(max-width: $break-small){
                .hidden{
                    display: none;
                }
                .visible{
                    top: 2.83rem;
                    right:0;
                    width:100%;
                    z-index:999;

                    ul{
                        padding:0;
                        li{
                            display: block;
                            border-bottom: 1px solid #ced0d0;
                            background:white;
                            font-size: 1.3em;
                            text-align:center;
                            height: 45px;
                            padding: 10px 0 0 0;
                        }
                    }
                }                
            }
        }

        &__logo {
            cursor: pointer;
        }
    }
</style>