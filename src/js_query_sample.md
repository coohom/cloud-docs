# Js Query Sample Code
World screening jsQuery sample

### World with more than 400 Objects
```javascript
function() {
    var count=0;
    for (var instance of this.instances) {
        if (instance.type == 'CC_OBJECT') {
            count ++;
        }
    }
    return count > 400;
}
```
 
### World containing "Carpet (label id 1080)"
```javascript
function() {
    for (var instance of this.instances) {
        if (instance.label && instance.label == 1080) {
            return true;
        }
    }
    return false;
}
```

### Furniture Label list

| label_id   | parent_label_id  | name_cn                   | name_en                                    |
| ---- | ---- | ------------------------- | ------------------------------------------ |
| 1000 | -1   | 软装                      | Soft decoration                            |
| 1001 | 1000 | 家具                      | Furniture                                  |
| 1002 | 1001 | 床                        | Beds                                       |
| 1003 | 1002 | 儿童床                    | Crib                                       |
| 1004 | 1002 | 单人床                    | Single bed                                 |
| 1005 | 1002 | 双人床                    | Double bed                                 |
| 1006 | 1002 | 婴儿床                    | Baby Bed                                   |
| 1007 | 1002 | 架子床                    | Bunk                                       |
| 1008 | 1002 | 组合床                    | Sectional bed                              |
| 1009 | 1002 | 高低床                    | High and low bed                           |
| 1010 | 1002 | 榻榻米                    | Tatami                                     |
| 1011 | 1002 | 其他床类                  | Other bed                                  |
| 1012 | 1001 | 架类                      | Shelf                                      |
| 1013 | 1012 | 鞋架                      | Shoe racks                                 |
| 1014 | 1012 | 书架                      | Bookshelves                                |
| 1015 | 1012 | 壁架                      | Ledge                                      |
| 1016 | 1012 | 陈列架                    | Display shelf                              |
| 1017 | 1012 | 衣帽架                    | Coat stands                                |
| 1018 | 1012 | 其他架类                  | Other shelves                              |
| 1019 | 1001 | 橱（柜）                  | Cabinet                                    |
| 1020 | 1019 | 衣橱（柜）                | Wardrobe                                   |
| 1021 | 1019 | 书橱（柜）                | bookcase                                   |
| 1022 | 1019 | 餐边橱（柜）              | Sideboard                                  |
| 1023 | 1019 | 床头橱（柜）              | Bedside cabinets                           |
| 1024 | 1019 | 电视橱（柜）              | TV stand                                   |
| 1025 | 1019 | 储物橱（柜）              | Storage cabinet                            |
| 1026 | 1025 | 办公柜                    | Office cabinet                             |
| 1027 | 1025 | 墙柜                      | Wall cabinet                               |
| 1028 | 1025 | 展柜                      | Showcase                                   |
| 1029 | 1025 | 酒柜                      | Wine cabinet                               |
| 1030 | 1025 | 鞋柜                      | Shoe cabinet                               |
| 1031 | 1019 | 其他柜类                  | Other cabinet                              |
| 1032 | 1001 | 桌子（台、几）            | Table                                      |
| 1033 | 1032 | 茶几                      | Side tables                                |
| 1034 | 1032 | 书桌                      | Desk                                       |
| 1035 | 1032 | 餐桌                      | Dining table                               |
| 1036 | 1035 | 方桌                      | Square table                               |
| 1037 | 1035 | 圆桌                      | Round table                                |
| 1038 | 1035 | 异形                      | special-shaped Pillow                      |
| 1039 | 1032 | 其他桌子                  | Other table                                |
| 1040 | 1039 | 儿童桌                    | Children's table                           |
| 1041 | 1039 | 办公桌                    | The executive desk                         |
| 1042 | 1041 | 职员桌                    | Staff table                                |
| 1043 | 1041 | 老板桌                    | Executive desk                             |
| 1044 | 1041 | 会议桌                    | Conference table                           |
| 1045 | 1032 | 吧台                      | Bar counter                                |
| 1046 | 1032 | 梳妆台                    | Dressing Table                             |
| 1047 | 1032 | 花几                      | Pergola                                    |
| 1048 | 1032 | 角几                      | Side table                                 |
| 1049 | 1032 | 背几                      | Sofa back table                            |
| 1050 | 1032 | 其他                      | Others                                     |
| 1051 | 1050 | 玄关台                    | Console Tables                             |
| 1052 | 1001 | 椅子                      | Chair                                      |
| 1053 | 1052 | 靠背椅                    | Backchair                                  |
| 1054 | 1053 | 休闲椅                    | Lounge chair                               |
| 1055 | 1053 | 餐椅                      | Dinning chair                              |
| 1056 | 1052 | 凳子                      | Stool                                      |
| 1057 | 1056 | 矮凳                      | low stool                                  |
| 1058 | 1056 | 长凳                      | Bench                                      |
| 1059 | 1056 | 折叠凳                    | Folding stool                              |
| 1060 | 1056 | 坐墩                      | Porcelain stool                            |
| 1061 | 1056 | 沙发凳                    | Sofa bench                                 |
| 1062 | 1056 | 梳妆凳                    | Dressing stool                             |
| 1063 | 1052 | 吧椅                      | Bar stool                                  |
| 1064 | 1052 | 床尾凳                    | End-of-bed stool                           |
| 1065 | 1052 | 办公椅                    | Chair                                      |
| 1066 | 1052 | 吊椅（吊篮）              | Hanging chair                              |
| 1067 | 1052 | 其他椅子                  | Other chair                                |
| 1068 | 1001 | 沙发                      | Sofa                                       |
| 1069 | 1068 | 单人沙发                  | One-seater sofa                            |
| 1070 | 1068 | 贵妃椅                    | Princess Chair                             |
| 1071 | 1068 | 双人沙发（单件）          | Two-seater sofa                            |
| 1072 | 1068 | 多人沙发（组合沙发）      | Multi seat sofa                            |
| 1073 | 1068 | High Tech 沙发            | High Tech Sofa                             |
| 1074 | 1068 | 懒人沙发 （软，无硬支撑） | Lazy sofa                                  |
| 1075 | 1068 | 榻类                      | Couch                                      |
| 1076 | 1068 | 其他沙发                  | Other sofa                                 |
| 1077 | 1001 | 屏风                      | Screens                                    |
| 1078 | 1001 | 其他家具                  | Other furniture                            |
| 1079 | 1000 | 软饰                      | Soft ornaments                             |
| 1080 | 1079 | 地毯                      | Carpet                                     |
| 1081 | 1079 | 坐垫                      | Cushion                                    |
| 1089 | 1079 | 床品                      | Bedding                                    |
| 1090 | 1089 | 被子                      | quilt                                      |
| 1091 | 1089 | 枕头                      | pillow                                     |
| 1092 | 1089 | 床旗                      | Bed flag                                   |
| 1093 | 1089 | 搭巾                      | Bed throws/                                |
| 1094 | 1079 | 窗帘                      | Curtain                                    |
| 1095 | 1094 | 纱帘                      | Sheer Curtains                             |
| 1096 | 1094 | 遮光帘                    | Shading curtain                            |
| 1097 | 1094 | 一片式窗帘                | One-piece curtain                          |
| 1098 | 1079 | 靠包                      | throw pillow                               |
| 1099 | 1098 | 抱枕（方）                | throw pillow                               |
| 1100 | 1098 | 腰靠（长）                | Lumbar pillow                              |
| 1101 | 1098 | 异形                      | special-shaped Pillow                      |
| 1102 | 1079 | 餐布                      | Tablecloth                                 |
| 1103 | 1102 | 桌布                      | tablecloth                                 |
| 1104 | 1102 | 餐垫                      | Table mat                                  |
| 1105 | 1102 | 餐巾                      | napkin                                     |
| 1106 | 1102 | 桌旗                      | Table runner                               |
| 1107 | 1000 | 家饰                      | House decoration                           |
| 1108 | 1107 | 挂画                      | Painting                                   |
| 1109 | 1108 | 国画书法                  | Traditional Chinese Painting & Handwriting |
| 1110 | 1108 | 手绘速写                  | Hand painted                               |
| 1111 | 1108 | 摄影                      | Photography                                |
| 1112 | 1108 | 油画                      | Painting                                   |
| 1113 | 1108 | 装饰画                    | Peinture decorative                        |
| 1114 | 1113 | 装置画                    | Stereograph                                |
| 1115 | 1113 | 抽象画                    | Abstract painting                          |
| 1116 | 1113 | 现代创意                  | Modern Creative Painting                   |
| 1117 | 1113 | 其他                      | Others                                     |
| 1118 | 1107 | 灯具                      | Light                                      |
| 1119 | 1118 | 台灯                      | Table Lamp                                 |
| 1120 | 1118 | 吊灯                      | Chandelier                                 |
| 1121 | 1118 | 吸顶灯                    | Ceiling mounted lamp                       |
| 1122 | 1118 | 壁灯                      | Wall lights                                |
| 1123 | 1118 | 射灯 （筒灯）             | Spotlight/Downlight                        |
| 1124 | 1118 | 落地灯                    | Floor Lamp                                 |
| 1125 | 1107 | 生活辅助                  | Articles for daily use                     |
| 1126 | 1125 | 厨具                      | Kitchenware                                |
| 1127 | 1126 | 炊具                      | Cooker                                     |
| 1128 | 1127 | 锅具                      | Cookware                                   |
| 1129 | 1127 | 刀具                      | Tooling                                    |
| 1130 | 1127 | 餐车                      | Dining car                                 |
| 1131 | 1127 | 其他（铲勺等）            | Other Cooker                               |
| 1132 | 1126 | 餐具                      | Bowl                                       |
| 1133 | 1132 | 碗                        | Bowl                                       |
| 1134 | 1132 | 筷                        | Chopsticks                                 |
| 1135 | 1132 | 杯（不含酒杯茶杯）        | Cup                                        |
| 1136 | 1132 | 碟                        | Plate                                      |
| 1261 | 1132 | 刀                        | Knife                                      |
| 1262 | 1132 | 勺                        | Spoon                                      |
| 1263 | 1132 | 叉                        | Fork                                       |
| 1137 | 1126 | 茶具                      | Tea set                                    |
| 1138 | 1126 | 酒具                      | Wine set                                   |
| 1139 | 1126 | 其他厨具                  | Other Kitchenware                          |
| 1140 | 1125 | 家电                      | House appliances                           |
| 1141 | 1140 | 大家电                    | Large appliance                            |
| 1142 | 1141 | 电视                      | TV                                         |
| 1143 | 1141 | 立式空调                  | Vertical air-conditioner                   |
| 1144 | 1141 | 挂式空调                  | Wall mounted air conditioner               |
| 1145 | 1141 | 冰箱                      | Fridge                                     |
| 1146 | 1141 | 洗衣机                    | Washing machine                            |
| 1147 | 1140 | 小家电                    | Small appliance                            |
| 1148 | 1147 | 电风扇                    | Electric fan                               |
| 1149 | 1147 | 饮水机                    | Water Coolers                              |
| 1150 | 1147 | 空气净化器                | Air purifier                               |
| 1151 | 1147 | 音响                      | Sound                                      |
| 1152 | 1147 | 挂烫机                    | Hanging ironing machine                    |
| 1153 | 1147 | 取暖器                    | Heater                                     |
| 1154 | 1147 | 吸尘器                    | Vacuum cleaner                             |
| 1155 | 1147 | 吊扇                      | Ceiling fan                                |
| 1156 | 1147 | 扫地机器人                | Sweeping robot                             |
| 1157 | 1140 | 厨房家电                  | Kitchen appliances                         |
| 1158 | 1157 | 抽油烟机                  | Smoke exhaust ventilator                   |
| 1159 | 1157 | 热水器                    | Water heater                               |
| 1160 | 1157 | 电磁炉                    | Induction cooker                           |
| 1161 | 1157 | 微波炉                    | Microwave oven                             |
| 1162 | 1157 | 面包机                    | Bread machine                              |
| 1163 | 1157 | 烧水壶                    | Kettle                                     |
| 1164 | 1157 | 榨汁机                    | Juice Maker                                |
| 1165 | 1157 | 咖啡机                    | Coffee maker                               |
| 1166 | 1157 | 洗碗机                    | Dishwasher                                 |
| 1167 | 1157 | 嵌入式烤箱                | Built-in oven                              |
| 1168 | 1157 | 电饭煲                    | Electric cooker                            |
| 1169 | 1140 | 其他家电                  | Other household appliances                 |
| 1170 | 1125 | 日用品                    | Daily Necessities                          |
| 1171 | 1170 | 收纳                      | Storage                                    |
| 1172 | 1170 | 玩具                      | Toys                                       |
| 1173 | 1170 | 生活用品                  | Articles for daily use                     |
| 1264 | 1173 | 乐器                      | Musical instrument                         |
| 1083 | 1264 | 钢琴                      | Piano                                      |
| 1266 | 1264 | 其他                      | Others                                     |
| 1084 | 1173 | 健身器材                  | Fitness equipment                          |
| 1085 | 1084 | 跑步机                    | Treadmill                                  |
| 1086 | 1084 | 其他健身器材              | Other fitness equipment                    |
| 1087 | 1084 | 自行车（包含健身器材）    | Bicycle                                    |
| 1268 | 1173 | 其他                      | Others                                     |
| 1174 | 1170 | 办公用品                  | Office supplies                            |
| 1175 | 1174 | 台式电脑                  | Desktop computer                           |
| 1176 | 1174 | 其他                      | Others                                     |
| 1177 | 1125 | 花卉绿植（特指植物）      | Flowers and plants                         |
| 1178 | 1177 | 花卉                      | Flowers & Plants                           |
| 1179 | 1178 | 挂壁花卉                  | Wallflower                                 |
| 1180 | 1178 | 摆放花卉                  | Flower                                     |
| 1181 | 1178 | 落地花卉                  | Floor flower                               |
| 1182 | 1177 | 绿植                      | Green plants                               |
| 1183 | 1182 | 挂壁绿植                  | Wall green plants                          |
| 1184 | 1182 | 摆放绿植                  | Green plants                               |
| 1185 | 1182 | 落地绿植                  | Floor green plants                         |
| 1186 | 1125 | 配饰                      | Aromatherapy                               |
| 1187 | 1186 | 书摆                      | Bookends                                   |
| 1188 | 1186 | 吊饰                      | Pendants                                   |
| 1189 | 1186 | 壁饰（墙饰/挂件）         | Wall decoration                            |
| 1190 | 1186 | 托盘                      | Tray                                       |
| 1191 | 1186 | 摆件                      | Ornament                                   |
| 1192 | 1191 | 装饰碗                    | Decorative bowl                            |
| 1193 | 1191 | 装饰盘                    | Decorative plate                           |
| 1194 | 1191 | 储物罐                    | Storage tank                               |
| 1195 | 1191 | 烟灰缸                    | Ashtray                                    |
| 1196 | 1191 | 鱼缸                      | Fish tank                                  |
| 1197 | 1191 | 其他                      | Others                                     |
| 1198 | 1186 | 时钟                      | Clock                                      |
| 1199 | 1186 | 烛台                      | Menorah                                    |
| 1200 | 1186 | 相框                      | Picture frame                              |
| 1201 | 1186 | 花器                      | Flower ware                                |
| 1202 | 1201 | 花盆                      | flower pot                                 |
| 1088 | 1201 | 花瓶                      | vase                                       |
| 1204 | 1186 | 装饰盒                    | Decorative box                             |
| 1205 | 1186 | 镜子                      | Mirror                                     |
| 1206 | 1205 | 普通镜                    | Ordinary mirror                            |
| 1207 | 1205 | 化妆镜                    | Cosmetic mirror                            |
| 1208 | 1205 | 浴室镜                    | Bathroom mirror                            |
| 1209 | 1205 | 穿衣镜                    | Dressing mirror                            |
| 1210 | 1205 | 试衣镜                    | Dressing mirror                            |
| 1211 | 1186 | 雕塑                      | Sculpture                                  |
| 1212 | 1186 | 香薰                      | Aromatherapy                               |
| 1213 | 1186 | 其他配饰                  | Other Aromatherapy                         |
| 1214 | -1   | 硬装                      | Hardware decoration                        |
| 1215 | 1214 | 硬装辅助                  | Hardware decoration                        |
| 1216 | 1215 | 门                        | Door                                       |
| 1217 | 1216 | 室内门                    | Interior door                              |
| 1218 | 1216 | 防盗门                    | Burglar-proof door                         |
| 1219 | 1216 | 推拉门                    | Sliding doors                              |
| 1220 | 1216 | 折叠门                    | Folding door                               |
| 1221 | 1215 | 窗                        | Window                                     |
| 1222 | 1221 | 飘窗                      | Bay window                                 |
| 1223 | 1221 | 推拉窗                    | Sliding window                             |
| 1224 | 1221 | 落地窗                    | French window                              |
| 1225 | 1221 | 平开窗                    | Casement window                            |
| 1226 | 1215 | 地面                      | Ground                                     |
| 1227 | 1226 | 地板                      | Floor                                      |
| 1228 | 1227 | 木地板                    | Wood floor                                 |
| 1229 | 1227 | 其他地板                  | Other floors                               |
| 1230 | 1226 | 地砖                      | Floor tile                                 |
| 1231 | 1230 | 瓷砖地面                  | Tile floor                                 |
| 1232 | 1230 | 其他地砖                  | Other floor tiles                          |
| 1233 | 1226 | 全屋地毯                  | Whole house carpet                         |
| 1234 | 1215 | 墙面                      | Wall                                       |
| 1235 | 1234 | 墙纸&墙布                 | Wallpaper & Wall cloth                     |
| 1236 | 1234 | 背景墙                    | Walls                                      |
| 1237 | 1234 | 其他墙面                  | Other Wall                                 |
| 1238 | 1215 | 顶面                      | Top surface                                |
| 1239 | 1215 | 楼梯                      | Stairs                                     |
| 1240 | 1215 | 卫浴                      | Bathroom                                   |
| 1241 | 1240 | 洗脸池                    | Inter-platform basin                       |
| 1242 | 1240 | 马桶                      | Closestool                                 |
| 1243 | 1240 | 便池                      | The toilet                                 |
| 1244 | 1240 | 洗浴缸                    | Bathtub                                    |
| 1245 | 1240 | 拖把池                    | Mop pool                                   |
| 1246 | 1240 | 其他卫浴用品              | Other Bathroom products                    |
| 1259 | 1215 | 柱                        | pillar                                     |
| 1260 | 1215 | 其他                      | Others                                     |
| 1247 | -1   | Avatar                    | Avatar                                     |
| 1248 | 1247 | 人物                      | Character                                  |
| 1249 | 1248 | 女性人物                  | Female                                     |
| 1250 | 1248 | 男性人物                  | Male                                       |
| 1251 | 1248 | 儿童人物                  | Children                                   |
| 1252 | 1251 | 男孩                      | Boy                                        |
| 1253 | 1251 | 女孩                      | Girl                                       |
| 1254 | 1247 | 动物                      | Animals                                    |
| 1255 | 1254 | 猫                        | Cat                                        |
| 1256 | 1254 | 狗                        | Dog                                        |
| 1257 | 1254 | 其他动物                  | Other pets                                 |
| 1258 | -1   | 其他                      | Others                                     |
