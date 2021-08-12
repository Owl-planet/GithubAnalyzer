<template>
    <div>
        <header data-aos="fade-down" data-aos-duration="900">
            <img class="logo" @click="ChangePageAH" alt="logo" src="https://img.icons8.com/dotty/80/000000/jellyfish.png"/>
            <nav>
                <ul class="nav__links">
                    <li><a @click="ChangePageAH">Home</a></li>
                    <li><a @click="ChangePageAGA">Github Analysis</a></li>
                    <li><a @click="ChangePageAA">About</a></li>
                </ul>
            </nav>
            <a class="cta" href="#"><button>Contact</button></a>
        </header>
    </div>
</template>

<script>
    export default{
        methods : {
            ChangePageAA(){
                this.$emit("CP", "app-about");
            },
            ChangePageAH(){
                this.$emit("CP", "app-section");
            },
            ChangePageAGA(){
                this.$emit("CP", "app-ag");
            },
        }
    }
</script>

<style scoped>
li,
a,
button {
  font-family: "Nunito", sans-serif;
  font-weight: 500;
  font-size: 16px;
  color: #edf0f1;
  text-decoration: none;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30px 10%;
}

.logo{
    cursor: pointer;
}

.nav__links{
    list-style:none;
}

.nav__links li{
    display: inline-block;
    padding: 0px 20px;
}
.nav__links li a{
    transition: all 0.3s ease 0s;
    cursor:pointer;
}

.nav__links li a:hover{
    color: #0088a9;
}

button{
    padding: 9px 25px;
    background-color: rgba(0, 136, 169, 1);
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease 0s;
}
button:hover{
    background-color: rgba(0, 136, 169, 0.8);
}
</style>