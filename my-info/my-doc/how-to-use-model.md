# 一、模型名与大小：

| 模型名称 | 磁盘空间 | 内存占用 | 适用设备 | 说明 |
|---------|----------|----------|----------|------|
| tiny.en | 71 MB | ~390 MB | 低端手机 | 专门用于英语识别，速度比tiny快30%，精确度最低 |
| tiny | 74 MB | ~390 MB | 低端手机 | 支持99种语言，速度最快，精确度最低。支持的语言，见【[语言编码](https://github.com/jims57/whisper.cpp/blob/master/my-info/my-doc/how-to-use-model.md#%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A0%81%E5%85%B199%E7%A7%8D%E8%AF%AD%E8%A8%80)】项 |
| base.en | 137 MB | ~500 MB | 中端手机 | 专门用于英语识别，速度比base快30%，精确度比tiny.en好 |
| base | 142 MB | ~500 MB | 中端手机 | 支持99种语言，速度较快，精确度比tiny好。支持的语言，见【[语言编码](https://github.com/jims57/whisper.cpp/blob/master/my-info/my-doc/how-to-use-model.md#%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A0%81%E5%85%B199%E7%A7%8D%E8%AF%AD%E8%A8%80)】项 |
| small.en | 447 MB | ~1.0 GB | 高端手机 | 专门用于英语识别，速度比small快30%，精确度均衡 |
| small | 466 MB | ~1.0 GB | 高端手机 | 支持99种语言，速度和精确度均衡。支持的语言，见【[语言编码](https://github.com/jims57/whisper.cpp/blob/master/my-info/my-doc/how-to-use-model.md#%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A0%81%E5%85%B199%E7%A7%8D%E8%AF%AD%E8%A8%80)】项 |
| medium | 1.5 GB | ~2.6 GB | 电脑（手机不适用） | 精确度较好，需要中端设备。支持的语言，见【[语言编码](https://github.com/jims57/whisper.cpp/blob/master/my-info/my-doc/how-to-use-model.md#%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A0%81%E5%85%B199%E7%A7%8D%E8%AF%AD%E8%A8%80)】项 |
| large | 2.9 GB | ~4.7 GB | 电脑（手机不适用） | 精确度最好，需要高端设备。支持的语言，见【[语言编码](https://github.com/jims57/whisper.cpp/blob/master/my-info/my-doc/how-to-use-model.md#%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A0%81%E5%85%B199%E7%A7%8D%E8%AF%AD%E8%A8%80)】项 |

备注：不带.en后缀的模型（tiny、base、small等）都支持【[语言编码](https://github.com/jims57/whisper.cpp/blob/master/my-info/my-doc/how-to-use-model.md#%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A0%81%E5%85%B199%E7%A7%8D%E8%AF%AD%E8%A8%80)】中所列的99种语言。

说明：
1. 模型越小，速度越快，但精确度更差。这类模型，合适用于低端手机。
2. 模型越大，速度越慢，精确度更好。这类模型，合适用于比较高端的手机。
3. 开发时，你先从模型小的开始测试，以便测试。
4. 不管是哪种模型，如果要保证推理速度，都要保证设备（如iPhone）有GPU或ANE，否则速度会很慢。所以，你最好在代码中检查设备是否有GPU或ANE。如果没有，则自动选择最小的模型（tiny或tiny.en）。
5. 关于选择哪些模型的逻辑，后台会根据传参自动选择，并提供下载链接。
6. 下载模型的流程图，见：<a href="https://docs.qq.com/flowchart/DZHhpTEdLcW9lT2VE" target="_blank">https://docs.qq.com/flowchart/DZHhpTEdLcW9lT2VE</a>

# 二、开发注意事项：
## 1. 测试多语言模型（如tiny、small等没有.en后缀的模型）时，记得要对应修改语言编码。
<img width="1096" alt="image" src="https://github.com/user-attachments/assets/784bb829-4699-42e3-9bed-adcbfffdf38a" />

## 2.发布时，不要把模型放到项目中，防止App太大。
<img width="955" alt="image" src="https://github.com/user-attachments/assets/dd486658-2509-400b-a645-04c5bd65962d" />

## 3.第一次加载后，推理会比较慢，往后就会快。所以，如果你想测试速度，请以第2次（或N次）为准。
如下是官方文档说明： 设备上的首次运行速度较慢，因为 ANE 服务会将 Core ML 模型编译为某种特定于设备的格式。后续运行速度会更快。（原文见截图）

<img width="796" alt="image" src="https://github.com/user-attachments/assets/2e8bd0bd-84b4-4382-9dfd-094755d10ba2" />

## 4.启用Real-time按钮，可进行实时推理。否则，要按Transcribe才会转录（非实时）。
<img width="633" alt="image" src="https://github.com/user-attachments/assets/445d4213-a04a-4b4d-beda-1450485c0b79" />

## 5.说中文时，默认显示为【繁体字】。需要开发者，用相应的库，转为【简体字】。
<img width="330" alt="image" src="https://github.com/user-attachments/assets/f88e4f5a-cea8-40e7-872b-98605444f6d1" />

## 6.如果Xcode缺少模型，请联系Jimmy。
<img width="449" alt="image" src="https://github.com/user-attachments/assets/7d33d1c5-3ce3-494f-8ea3-a5de7742c9f6" />




# 三、语言编码（共99种语言）：
| 编号 | 代码 | 语言 |
|------|------|------|
| 1 | af | 南非荷兰语 |
| 2 | am | 阿姆哈拉语 |
| 3 | ar | 阿拉伯语 |
| 4 | as | 阿萨姆语 |
| 5 | az | 阿塞拜疆语 |
| 6 | ba | 巴什基尔语 |
| 7 | be | 白俄罗斯语 |
| 8 | bg | 保加利亚语 |
| 9 | bn | 孟加拉语 |
| 10 | bo | 藏语 |
| 11 | br | 布列塔尼语 |
| 12 | bs | 波斯尼亚语 |
| 13 | ca | 加泰罗尼亚语 |
| 14 | cs | 捷克语 |
| 15 | cy | 威尔士语 |
| 16 | da | 丹麦语 |
| 17 | de | 德语 |
| 18 | el | 希腊语 |
| 19 | en | 英语 |
| 20 | es | 西班牙语 |
| 21 | et | 爱沙尼亚语 |
| 22 | eu | 巴斯克语 |
| 23 | fa | 波斯语 |
| 24 | fi | 芬兰语 |
| 25 | fo | 法罗语 |
| 26 | fr | 法语 |
| 27 | gl | 加利西亚语 |
| 28 | gu | 古吉拉特语 |
| 29 | ha | 豪萨语 |
| 30 | haw | 夏威夷语 |
| 31 | he | 希伯来语 |
| 32 | hi | 印地语 |
| 33 | hr | 克罗地亚语 |
| 34 | ht | 海地克里奥尔语 |
| 35 | hu | 匈牙利语 |
| 36 | hy | 亚美尼亚语 |
| 37 | id | 印度尼西亚语 |
| 38 | is | 冰岛语 |
| 39 | it | 意大利语 |
| 40 | ja | 日语 |
| 41 | jw | 爪哇语 |
| 42 | ka | 格鲁吉亚语 |
| 43 | kk | 哈萨克语 |
| 44 | km | 柬埔寨语 |
| 45 | kn | 卡纳达语 |
| 46 | ko | 韩语 |
| 47 | la | 拉丁语 |
| 48 | lb | 卢森堡语 |
| 49 | ln | 林加拉语 |
| 50 | lo | 老挝语 |
| 51 | lt | 立陶宛语 |
| 52 | lv | 拉脱维亚语 |
| 53 | mg | 马达加斯加语 |
| 54 | mi | 毛利语 |
| 55 | mk | 马其顿语 |
| 56 | ml | 马拉雅拉姆语 |
| 57 | mn | 蒙古语 |
| 58 | mr | 马拉地语 |
| 59 | ms | 马来语 |
| 60 | mt | 马耳他语 |
| 61 | my | 缅甸语 |
| 62 | ne | 尼泊尔语 |
| 63 | nl | 荷兰语 |
| 64 | nn | 新挪威语 |
| 65 | no | 挪威语 |
| 66 | oc | 奥克语 |
| 67 | pa | 旁遮普语 |
| 68 | pl | 波兰语 |
| 69 | ps | 普什图语 |
| 70 | pt | 葡萄牙语 |
| 71 | ro | 罗马尼亚语 |
| 72 | ru | 俄语 |
| 73 | sa | 梵语 |
| 74 | sd | 信德语 |
| 75 | si | 僧伽罗语 |
| 76 | sk | 斯洛伐克语 |
| 77 | sl | 斯洛文尼亚语 |
| 78 | sn | 绍纳语 |
| 79 | so | 索马里语 |
| 80 | sq | 阿尔巴尼亚语 |
| 81 | sr | 塞尔维亚语 |
| 82 | su | 巽他语 |
| 83 | sv | 瑞典语 |
| 84 | sw | 斯瓦希里语 |
| 85 | ta | 泰米尔语 |
| 86 | te | 泰卢固语 |
| 87 | tg | 塔吉克语 |
| 88 | th | 泰语 |
| 89 | tk | 土库曼语 |
| 90 | tl | 他加禄语 |
| 91 | tr | 土耳其语 |
| 92 | tt | 鞑靼语 |
| 93 | uk | 乌克兰语 |
| 94 | ur | 乌尔都语 |
| 95 | uz | 乌兹别克语 |
| 96 | vi | 越南语 |
| 97 | yi | 意第绪语 |
| 98 | yo | 约鲁巴语 |
| 99 | zh | 中文 |
