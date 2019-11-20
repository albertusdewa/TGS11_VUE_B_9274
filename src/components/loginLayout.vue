<template>
        <v-app>
            <v-content>
                <v-container class="fill-height" fluid>
                    <v-row  justify="center">
                        <div class="form">
                            <v-text-field
                                v-model="form.email"
                                label="Email"
                                filled
                            ></v-text-field>
                            <v-text-field
                                v-model="form.password"
                                label="Password"
                                filled
                                :type="show1 ? 'text' : 'password'"
                            ></v-text-field>
                            <v-checkbox v-model="checkbox" style="margin-top : -10px">
                                <template v-slot:label>
                                    <div>
                                        Remember me
                                    </div>
                                </template>
                            </v-checkbox>
                            <v-btn @click="login()" block color="white" class="elevation-0" >Login</v-btn>
                        </div>
                    </v-row>
                </v-container>
            </v-content>
        </v-app>
</template>

<script>
export default {
    data(){
        return {
            form : {
                email: null, 
                password: null,
            },
            user : new FormData,
        }
    },
    methods:{
        login(){
            var url = this.$apiUrl + '/auth'
            this.user = new FormData()
            this.user.append('email',this.form.email);
            this.user.append('password',this.form.password);
            this.$http.post(url,this.user).then(response =>{
                if(response.data.token){
                    localStorage.setItem("token" , response.data.token)
                this.$router.push({ name : "UserController"})
                }else{
                    alert('gagal login')
                }
            })
        }
    }
}
</script>

<style>
.form{
    margin-left: -200px;
    margin-top: 0px;
    margin-bottom: 20px;
    color: rgba(0, 0, 0, 0.54);
}
</style>