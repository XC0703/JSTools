在需要将表单数据导出的组件只需用到以下函数即可到传入的数据导出为表格：（表格的列属性自定义）
```javascript
// 导出为表格
const handleExport = (wareList)=>{
    import('@/utils/exportExcel').then(excel => {
        const res = []
        // excel表示导入的模块对象
        for(let i =0;i<wareList.length;i++){
            delete wareList[i].id
            res.push(wareList[i])
        }
        // const one = res[0] // 返回的数组取第一项
        // const header = Object.keys(one) // 拿对象中的所有的键
        const header = ['物品id','物品名称','物品价格','库存数量','创建时间','更新时间']
        const data = res.map(item => Object.values(item)) //拿到里面的每一个值
        excel.export_json_to_excel({
            header, // 表头 必填
            data, // 具体数据 必填
            filename: 'wareList', // 文件名称
            autoWidth: true, // 宽度是否自适应
            bookType: 'xlsx' // 生成的文件类型
        })
    })
}
```
