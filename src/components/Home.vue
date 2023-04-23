<template>
    <div>
        <el-select v-model="selectType" placeholder="请选择组件类型">
            <el-option v-for="item in selectionsType" :key="item.value" :label="item.label" :value="item.value">
            </el-option>
        </el-select>
        <el-select v-model="selectPosition" placeholder="请选择组件位置">
            <el-option v-for="item in selectionsPosition" :key="item.value" :label="item.label" :value="item.value">
            </el-option>
        </el-select>
        <el-form label-width="80px" :model="content">
            <el-form-item :label="options.sys">
                <el-input type="textarea" v-model="content.sys"></el-input>
            </el-form-item>
            <el-form-item :label="options.plugname">
                <el-input type="textarea" v-model="content.plugname"></el-input>
            </el-form-item>
            <el-form-item :label="options.plugtype">
                <el-input type="textarea" v-model="content.plugtype"></el-input>
            </el-form-item>

            <el-form-item :label="options.comname">
                <el-input type="textarea" v-model="content.comname"></el-input>
            </el-form-item>
            <el-form-item :label="options.comcode">
                <el-input type="textarea" v-model="content.comcode"></el-input>
            </el-form-item>
            <el-form-item :label="options.comparam">
                <el-input type="textarea" v-model="content.comparam" :rows="5"></el-input>
            </el-form-item>

            <el-form-item :label="options.uicfg">
                <el-input type="textarea" v-model="content.uicfg" :rows="4"></el-input>
            </el-form-item>
            <el-form-item :label="options.zindex">
                <el-input type="textarea" v-model="content.zindex"></el-input>
            </el-form-item>
        </el-form>
        <el-button type="primary" @click="generateSQL">生成sql语句</el-button>
        <el-input type="textarea" v-model="sqlcode" :rows="10"></el-input>
    </div>
</template>

<script>
export default {
    methods: {
        generateSQL() {
            const pre = `INSERT INTO cx_plugincoms(sys,plugname,plugtype,comname,comcode,comparam,uicfg,zindex)
VALUES (`
            const last = `)`
            const content = `\"${this.content.sys}\", \"${this.content.plugname}\", \"${this.content.plugtype}\", \"${this.content.comname}\", \"${this.content.comcode}\", \'${this.content.comparam}\', \'${this.content.uicfg}\', ${this.content.zindex}`
            const sql = pre + content + last
            this.sqlcode = sql
        }
    },
    watch: {
        selectType(value) {
            switch (value) {
                case 'SimpleBar':
                    this.content.comparam = `{"title": "农民合作社", "border":1,"barColor": [{"offset": 0, "color": "#42f587"}],"xAxis":{"axisLabel":{"color":"#fff"},"axisLine":{"show":true}},"yAxis":{"axisLine":{"show":true,"lineStyle":{"color":"#fff","width":1}},"axisTick":{"show":true,"interval":"auto","inside":false,"length":5,"lineStyle":{"color":"#fff","width":1}},"splitLine":{"show":true,"lineStyle":{"type":"dashed","color":"#ccc"}},"axisLabel":{"show":true,"interval":"auto","margin":10,"textStyle":{"color":"#fff"}}},"series":{"barWidth":25},"sourceparam":{"data":[{"name":"农业","value":68984},{"name":"畜牧业","value":100815},{"name":"渔业","value":49548},{"name":"林业","value":137138},{"name":"服务业","value":18011}]}}`
                    break;
            
                default:
                    break;
            }
        },
        selectPosition(value) {
            switch (value) {
                case "1":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"13%","left":"10px"}`
                    break;
            
                default:
                    break;
            }
        }
    },
    data() {
        return {
            sqlcode: "",
            selectPosition: "",
            selectionsPosition: [{
                value: '1',
                label: '1'
            }, {
                value: '2',
                label: '2'
            }, {
                value: '3',
                label: '3'
            }, {
                value: '4',
                label: '4'
            }, {
                value: '5',
                label: '5'
            },{
                value: '6',
                label: '6'
            },{
                value: '7',
                label: '7'
            }],
            selectionsType: [{
                value: 'SimpleBar',
                label: 'SimpleBar'
            }, {
                value: 'SimpleLine',
                label: 'SimpleLine'
            }, {
                value: 'MultipleLine',
                label: 'MultipleLine'
            }, {
                value: 'BjTab',
                label: 'BjTab'
            }, {
                value: 'SimpleTab2',
                label: 'SimpleTab2'
            }],
            selectType: '',
            options: {
                sys: "sys",
                plugname: "plugname",
                plugtype: "plugtype",
                comname: "comname",
                comcode: "comcode",
                comparam: "comparam",
                uicfg: "uicfg",
                zindex: "zindex"
            },
            content: {
                sys: "11",
                plugname: "Rkzy1",
                plugtype: "1",
                comname: "SimpleBar",
                comcode: "Rkzy1-chart1",
                comparam: "",
                uicfg: "",
                zindex: 1
            }
        }
    }
}
</script>
<style></style>