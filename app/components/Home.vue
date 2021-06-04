<template>
    <Page  class="app">
     <ActionBar class='header' title="Calculator"/>
         <GridLayout class="keyboard" columns="*, *, *, *" rows="*, *, *, *, *, *">
            <Label textWrap="true" class="result" v-model="result" row="0" col="0" colSpan="4"/>/>
            <Button  class="button act" text="Clear" @tap="del()" row="1" col="0" colSpan="3"/>
            <Button  class="button act" text="/" @tap="input('/')" row="1" col="3"/>
            <Button  class="button" text="7" @tap="input('7')" row="2" col="0"/>
            <Button  class="button" text="8" @tap="input('8')" row="2" col="1"/>
            <Button  class="button" text="9" @tap="input('9')" row="2" col="2"/>
            <Button  class="button act" text="*" @tap="input('*')" row="2" col="3"/>
            <Button  class="button" text="4" @tap="input('4')" row="3" col="0"/>
            <Button  class="button" text="5" @tap="input('5')" row="3" col="1"/>
            <Button  class="button" text="6" @tap="input('6')" row="3" col="2"/>
            <Button  class="button act" text="-" @tap="input('-')" row="3" col="3"/>
            <Button  class="button" text="1" @tap="input('1')" row="4" col="0"/>
            <Button  class="button" text="2" @tap="input('2')" row="4" col="1"/>
            <Button  class="button" text="3" @tap="input('3')" row="4" col="2"/>
            <Button  class="button act" text="+" @tap="input('+')" row="4" col="3"/>
            <Button  class="button" text="0" @tap="input('0')" row="5" col="0" colSpan="2"/>
            <Button  class="button" text="." @tap="input('.')" row="5" col="2"/>
            <Button  class="button act" text="=" @tap="calc()" row="5" col="3" />
         </GridLayout>
    </Page>
</template>

<script >
    let invalid = 'Invalid!';
    let operation = false;
    let point = false;
    export default  {
    data() {
        return {
            result: '',
      }
    },
    methods:{
            input: function(char){
                this.result = this.result.toString();
                if (this.result === invalid){
                    this.result = '';
                }
                if ((char === '+' || char === '/' || char === '-' || char === '*') && operation === false){
                    operation = true;
                    point = false;
                    this.result += char;
                }
                else if(char === '.' && point === false){
                    operation = true;
                    point = true;
                    this.result += char;
                }
                else if ((char === '0' || char === '1' || char === '2' || char === '3' || char === '4' || 
                          char === '5' || char === '6' || char === '7' || char === '8' || char === '9')){
                    operation = false;                   
                    this.result += char;
                }
            },
            calc: function(){
                try{
                    this.result = eval(this.result);
                    if (isNaN(this.result)) {
                        throw new Error();
                  }
                }
                catch{
                    this.result = 'Invalid!';
                }
            },
            
            del: function(){
                this.result = ''
                operation = false;
                point = false;
            }
    }
  }
</script>

<style scoped>
    .header{
        background-color: #000;
        color: #fff;
    }
    .app{
        background-color: #474747;
    }
    .result{
        text-align: right;
        font-size: 28px;
        overflow-wrap: break-word;
        color: #fff;
    }
    .button{
        background-color: #fff;
        color: #000;
        border: solid;
        border-width: 2px;
        border-color: #000;
        width: 360px;
        height: 360px;
    }
    .button[text="Clear"]{
        width: 1080px;
    }
    .button[text='0']{
        width: 720px;
    }
    .button:active {
         background-color: #ebae08;
    }
    .act {
        background-color: #33f393;
    }
    .act:active {
        background-color: #fff;
    }
</style>
