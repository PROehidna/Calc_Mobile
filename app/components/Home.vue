<template>
    <Page class="page">
        <ActionBar title="Calculator" class="action-bar" />
        <GridLayout columns="100,100,100,*" rows="5,39,50,50,100,100,100,100,*">

            <Label  class="input1" row="1" col="0" colSpan="4" v-model="ev"  />
            <Label  class="input2" row="2" col="0" colSpan="4" v-model="result" />

            <Button class="btn5" row="3" col="0" text="(" @tap="val('(')" />
            <Button class="btn5" row="3" col="1" text=")" @tap="val(')')" />

            <Button class="btn2" row="4" col="0" text="C" @tap="cls" />    
            <Button v-if="ev" class="btn2" row="4" col="1" text="<--" @tap="clrlast" />
            <Button class="btn2" row="4" col="2" text="/" @tap="val('/')" />
            <Button class="btn2" row="4" col="3" text="*" @tap="val('*')" />

            <Button class="btn" row="5" col="0" text="7" @tap="val('7')" />
            <Button class="btn" row="5" col="1" text="8" @tap="val('8')"/>
            <Button class="btn" row="5" col="2" text="9" @tap="val('9')" />
            <Button class="btn2" row="5" col="3" text="-" @tap="val('-')" />

            <Button class="btn" row="6" col="0" text="4" @tap="val('4')" />
            <Button class="btn" row="6" col="1" text="5" @tap="val('5')" />
            <Button class="btn" row="6" col="2" text="6" @tap="val('6')" />
            <Button class="btn2" row="6" col="3" text="+" @tap="val('+')" />

            <Button class="btn" row="7" col="0" text="1" @tap="val('1')" />
            <Button class="btn" row="7" col="1" text="2" @tap="val('2')" />
            <Button class="btn" row="7" col="2" text="3" @tap="val('3')" />
            <Button class="btn2 btn3" row="7" col="3" text="=" rowSpan="2" @tap="calcit" />/>

            <Button class="btn btn4" row="8" col="0" text="0" colSpan="2" @tap="val('0')" />/>
            <Button class="btn" row="8" col="2" text="." @tap="val('.')" />/>

        </GridLayout>
    </Page>
</template>

<script>
    export default {
        data() {
            return {
                ev: '',
                result: '',
            }
        },
        methods: {
            val: function(p) {
                this.result = '';
                this.ev += p;
            },
            cls: function() {
                this.result = '';
                this.ev = '';
            },
            clrlast: function() {
                this.result = '';
                this.ev = this.ev.slice(0, -1);
            },
            calcit: function() {
                try {
                    this.result = eval(this.ev);
                } catch(err) {
                    this.result = 'ERR'
                }
            }
        }
    };
</script>

<style scoped>
.btn, .btn2, .btn3, .btn4, .btn5 {
    background-color: #6699ff;
    color: #ffffff;
    font-size: 24;
    width: 80;
    height: 80;
    border: 0;
    border-radius: 40;
}
.btn2 {
    background-color: #009900;
}
.btn3 {
    height: 180;
}
.btn4 {
    width: 180;
}
.btn5 {
    font-size: 15;
    width: 80;
    height: 40;
    border-radius: 25;
}
.input1, .input2 {
    border-width: 2;
    border-bottom-width: 0;
    border-color: #000000;
    background-color: #ffffff;
    margin: 10;
    padding: 5 10 5 10;
    height: 39;
    color: black;
    font-size:20;
    text-align: right;
}
.input2 {
    border-bottom-width: 2;
    border-top-width: 0;
    padding: 0 5 0 0;
    height: 50;
    font-size: 35;
}
</style>