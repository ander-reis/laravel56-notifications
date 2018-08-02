<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 col-md-offset-2">
                <div class="panel panel-default">
                    <div class="panel-heading">Notificações</div>

                    <div class="panel-body">
                        <ul>
                            <li v-for="notification in notifications">{{ notification.message }}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['user'],
        data() {
            return {
                notifications: []
            }
        },
        mounted() {
            Echo.private('App.User.' + this.user)
                .notification((notification) => {
                    this.notifications.push(notification);
                    let not = new Notification(notification.message, {
                        icon: 'http://logonoid.com/images/laravel-logo.png'
                    });
                    console.log(notification);
                    console.log('component Mounted');
                    not.onclick = () => {
                        window.open('https://schoolofnet.com');
                    }
                })
        }
    }
</script>
