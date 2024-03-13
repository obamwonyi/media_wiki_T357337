<script setup>
import '../../assets/js/header';
import router from '@/router';

//home view
function home()
{
    router.push("/");
}

//bug fix view
function bugFix()
{
    router.push("/bugfix");
}

</script>

<template>
    <div>
        <header class="header">
            <nav class="nav">
                <a class="brand" target="_blank" href="https://phabricator.wikimedia.org/T357337" >T357337</a>
                <div class="nav-links-div">
                    <ul class="nav-links-ul">
                        <li><a @click="home()">Home</a></li>
                        <li><a target="_blank" href="https://www.linkedin.com/in/destiny-obamwonyi-3a8a52218/">About Me</a></li>
                        <li><a @click="bugFix()">Bug Fix</a></li>
                        <li><a target="_blank" href="https://github.com/obamwonyi">Skill Set</a></li>
                    </ul>
                </div>
                <a class="discover" target="_blank" href="https://phabricator.wikimedia.org/p/Soda/">Mentor</a>
            </nav>
        </header>
    </div>
</template>

<style scoped>
@import '/src/assets/css/header.css';
</style>