<template>
    <div>
        <button class="btn btn-success ml-5 mt-5 mb-5" @click="getUserInfo">1. Get User Infos</button>
        <button class="btn btn-success ml-4 mt-5 mb-5" @click="getChart">2. Run</button><br>
        <span class="ml-5">1. User : <span style="color:green;">{{isReadyFU}}</span></span> <input class="input-group-text ml-5 mb-2" v-model.lazy="firstUser" style="background-color:black;color:white;" type="text">
        <span class="ml-5">2. User : <span style="color:green;">{{isReadySU}}</span></span> <input class="input-group-text ml-5 mt-2" v-model.lazy="secondUser" style="background-color:black;color:white;" type="text">
        <canvas  id="radar-chart" width="800" height="600"></canvas>
    </div>
</template>
<script>
const Chart = window.Chart;
export default{
    data(){
        return {
            isReadyFU : "",
            isReadySU : "",
            firstUser : "",
            secondUser : "",
            firstUserForOutput : "",
            secondUserForOutput : "",
            FirstUserPublicRepos : "",
            SecondUserPublicRepos : "",
            firstUserFollowers : "",
            secondUserFollowers : "",
            firstUserFollowing : "",
            secondUserFollowing : "",

            firstUserPublicGists : "",
            secondUserPublicGists : "",

            firstUserCreatedAt : "",
            secondUserCreatedAt : ""
        }
    },
    methods : {
        getUserInfo(){
            this.isReadyFU = "";
            this.isReadySU = "";
            let vm = this;
            let FirstUserPublicReposLocal = "";  // Ok
            let SecondUserPublicReposLocal = "";  // Ok
            let firstUserFollowersLocal = ""; // OK
            let secondUserFollowersLocal = ""; // ok
            let firstUserFollowingLocal = ""; // Ok
            let secondUserFollowingLocal = ""; // ok


            let firstUserCreatedAtLocal = "";
            let secondUserCreatedAtLocal = "";

            let firstUserPublicGistsLocal = ""; // ok
            let secondUserPublicGistsLocal = ""; // ok

            let firstUserName = ""; // ok
            let secondUserName = ""; // ok
            function islem2() {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                try {
                    fetch("https://api.github.com/users/" + vm.firstUser)
                        .then(function (response) {
                            return response.json();
                        }).then(function (response) {
                            console.log(response)
                            firstUserName = response.login;
                            firstUserCreatedAtLocal = response.created_at;
                            firstUserPublicGistsLocal = response.public_gists;
                            FirstUserPublicReposLocal = response.public_repos;
                            firstUserFollowersLocal = response.followers;
                            firstUserFollowingLocal = response.following;
                        });
                    resolve();
                } catch (hata) {
                    reject(hata);
                }
            }, 2000);
        });
    }
    function yazdir2() {
        setTimeout(() => {
            vm.firstUserCreatedAt = firstUserCreatedAtLocal;
            vm.firstUserPublicGists = firstUserPublicGistsLocal;
            vm.firstUserForOutput = firstUserName;
            vm.FirstUserPublicRepos = FirstUserPublicReposLocal;
            vm.firstUserFollowers = firstUserFollowersLocal;
            vm.firstUserFollowing = firstUserFollowingLocal;
            vm.isReadyFU = "Ready";
            console.log(FirstUserPublicReposLocal)
        }, 1000);
    }

    islem2()
        .then(yazdir2)
        // İslem 1
            function islem1() {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                try {
                    fetch("https://api.github.com/users/" + vm.secondUser)
                        .then(function (response) {
                            return response.json();
                        }).then(function (response) {
                            console.log(response)
                            secondUserCreatedAtLocal = response.created_at;
                            SecondUserPublicReposLocal = response.public_repos;
                            secondUserPublicGistsLocal = response.public_gists;
                            secondUserName = response.login;
                            secondUserFollowersLocal = response.followers;
                            secondUserFollowingLocal = response.following;
                        });
                    resolve();
                } catch (hata) {
                    reject(hata);
                }
            }, 2000);
        });
    }
    function yazdir1() {
        setTimeout(() => {
            vm.secondUserCreatedAt = secondUserCreatedAtLocal;
            vm.secondUserForOutput = secondUserName;
            vm.secondUserPublicGists = secondUserPublicGistsLocal;
            vm.SecondUserPublicRepos = SecondUserPublicReposLocal;
            vm.secondUserFollowers = secondUserFollowersLocal;
            vm.secondUserFollowing = secondUserFollowingLocal;
            console.log(SecondUserPublicReposLocal)
            vm.isReadySU = "Ready";
        }, 1000);
    }

    islem1()
        .then(yazdir1)
        },
        getChart(){
            new Chart(document.getElementById("radar-chart"), {
    type: 'radar',
    data: {
      labels: ["Public Repos", "Followers", "Public Gists", "Created At", "Following"],
      datasets: [
        {
          label: this.firstUserForOutput,
          fill: true,
          backgroundColor: "rgba(179,181,198,0.2)",
          borderColor: "rgba(179,181,198,1)",
          pointBorderColor: "#fff",
          pointBackgroundColor: "rgba(179,181,198,1)",
          data: [this.FirstUserPublicRepos,this.firstUserFollowers,this.firstUserPublicGists,this.firstUserCreatedAt.slice(0,4)/100,this.firstUserFollowing]
        }, {
          label: this.secondUserForOutput,
          fill: true,
          backgroundColor: "rgba(255,99,132,0.2)", // Alan içi
          borderColor: "rgba(255,99,132,1)", // alan kenarı
/*           pointBorderColor: "#fff", */
          pointBackgroundColor: "rgba(255,99,132,1)", 
          pointBorderColor: "#fff", 
          data: [this.SecondUserPublicRepos,this.secondUserFollowers,this.secondUserPublicGists,this.secondUserCreatedAt.slice(0,4)/100,this.secondUserFollowing]
        }
      ]
    },
    options: {
      title: {
        display: true,
        text: 'Output of Github Analysis'
      }
    }
});

        }
    }
}
            
</script>
<style scoped>
*{
    color:white;
}
h1{
    text-align: center;
    font-family: 'Courier New', Courier, monospace;
    color:white;
}
input{
    position: relative;
    display: block;
}
#radar-chart{
    display: block;
    margin-bottom: 500px;
}
</style>