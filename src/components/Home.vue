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
                <el-select v-model="content.plugname" placeholder="请选择插件名称">
                    <el-option v-for="item in plugnames" :key="item.value" :label="item.label" :value="item.value">
                    </el-option>
                </el-select>
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
                    this.content.comname = "SimpleBar"
                    this.content.comparam = `{"title": "农民合作社", "border":1,"barColor": [{"offset": 0, "color": "#42f587"}],"xAxis":{"axisLabel":{"color":"#fff"},"axisLine":{"show":true}},"yAxis":{"axisLine":{"show":true,"lineStyle":{"color":"#fff","width":1}},"axisTick":{"show":true,"interval":"auto","inside":false,"length":5,"lineStyle":{"color":"#fff","width":1}},"splitLine":{"show":true,"lineStyle":{"type":"dashed","color":"#ccc"}},"axisLabel":{"show":true,"interval":"auto","margin":10,"textStyle":{"color":"#fff"}}},"series":{"barWidth":25},"sourceparam":{"data":[{"name":"农业","value":68984},{"name":"畜牧业","value":100815},{"name":"渔业","value":49548},{"name":"林业","value":137138},{"name":"服务业","value":18011}]}}`
                    break;
                case 'SimpleLine':
                    this.content.comname = "SimpleLine"
                    this.content.comparam = `{"title": "垃圾清运", "border":1,"series":{"areaStyle":{"opacity":0}},"dw":"吨","sourceparam":{"data":[{"name":"周一","value":40},{"name":"周二","value":40},{"name":"周三","value":40},{"name":"周四","value":40},{"name":"周五","value":40},{"name":"周六","value":40},{"name":"周日","value":40}]}}`
                    break;
                case 'MultipleLine':
                this.content.comname = "MultipleLine"
                    this.content.comparam = `{"title": "流域水质变化", "border":1,"sourceparam":{"data":[{"name":"白沙河小学","value":[120,132,101,134,156]},{"name":"向家河","value":[260,182,191,264,156]},{"name":"泗湘溪","value":[260,182,191,264,156]},{"name":"长沙坝","value":[260,182,191,264,156]}]},"xdata": ["2019","2020","2021","2022","2023"]}`
                    break; 
                case 'BjTab':
                    this.content.comname = "BjTab"
                    this.content.comparam = `{"title": "土地面积概览", "border":1,"sourceparam":{"data":[{"name":"东西长度","value":"66公里"},{"name":"南北宽度","value":"54公里"},{"name":"总面积","value":"2327平方公里"}, {"name":"6镇2乡","value":"1311平方公里"}]}}`
                    break;
                case 'SimpleTab2':
                    this.content.comname = "SimpleTab2"
                    this.content.comparam = `{"title": "现代农业建设", "border":1,"sourceparam":{"data":[["高山商品蔬菜","6.5万亩", "10%"],["优质烟叶","3.1万亩", "15%"],["高标准农田","2万亩","21%"]]},"thData":["类别","数量","同比"]}`
                    break;
                default:
                    this.content.comname = ""
                    this.content.comparam = ""
                    break;
            }
        },
        selectPosition(value) {
            switch (value) {
                case "1":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"13%","left":"10px"}`
                    break;
                case "2":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"42%","left":"10px"}`
                    break
                case "3":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"71%","left":"10px"}`
                    break
                case "4":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"13%","right":"10px"}`
                    break
                case "5":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"42%","right":"10px"}`
                    break
                case "6":
                    this.content.uicfg = `{"width": "24%","height": "28%","top":"71%","right":"10px"}`
                    break
                case "7":
                    this.content.uicfg = `{"width": "25%","height": "28%", "top":"71%", "left":"calc(24% + 0.15rem)"}`
                    break
                case "8":
                    this.content.uicfg = `{"width": "25%","height": "28%", "top":"71%", "left":"calc(49% + 0.2rem)"}`
                    break
                default:
                    break;
            }
        }
    },
    data() {
        return {
            sqlcode: "",
            selectPosition: "",
            plugnames: [
                {
                    value: 'Rkzy1',
                    label: 'Rkzy1'
                },
                {
                    value: 'Rkzy2',
                    label: 'Rkzy2'
                },
                {
                    value: 'Rkzy3',
                    label: 'Rkzy3'
                }
            ],
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
            }, {
                value: '6',
                label: '6'
            }, {
                value: '7',
                label: '7'
            }, {
                value: '8',
                label: '8'
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
                plugname: "",
                plugtype: "1",
                comname: "",
                comcode: "",
                comparam: "",
                uicfg: "",
                zindex: 1
            }
        }
    }
}
</script>
<style></style>