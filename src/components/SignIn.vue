<template>
    <div class="ui text container">
        <div class="ui center aligned grid">
            <div class="column">
                <form class="ui large form">
                    <div class="ui stacked">
                        <div class="field">
                            <div class="ui left icon input">
                                <i class="user icon"></i>
                                <input type="text" name="email" placeholder="E-mail address">
                            </div>
                        </div>
                        <div class="field">
                            <div class="ui left icon input">
                                <i class="lock icon"></i>
                                <input type="password" name="password" placeholder="Password">
                            </div>
                        </div>
                        <div class="ui teal button">Sign In</div>
                    </div>
                </form>
                <div class="ui horizontal divider">
                    Or
                </div>
                <div class="ui google plus labeled icon button">
                    Sign in with Google+
                    <i class="google plus icon"></i>
                </div>
            </div>
        </div>
    </div>
</template>