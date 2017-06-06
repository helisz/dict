/*==============================================================*/
/* DBMS name: MySQL 5.0 */
/* Created on: 2017/3/5 10:29:05 */
/*==============================================================*/

```sql
drop table if exists Address;

drop table if exists ArticleComment;

drop table if exists ArticleType;

drop table if exists Articles;

drop table if exists DictSub;

drop table if exists DictTop;

drop table if exists OrderPdt;

drop table if exists Orders;

drop table if exists ProductComment;

drop table if exists Products;

drop table if exists Users;
```

/*==============================================================*/
/* Table: Address */
/*==============================================================*/
create table Address
(
 `AddressId` int not null auto_increment comment '收货地址编号',
 `UserId` int not null comment '用户编号',
 `Province` varchar(50) not null comment '省',
 `City` varchar(50) not null comment '市',
 `County` varchar(50) not null comment '县/区',
 `Street` varchar(300) not null comment '详细地址',
 `RevName` varchar(30) not null comment '收货人姓名',
 `PostCode` varchar(20) comment '邮政编码',
 `Mobile` varchar(50) not null comment '手机',
 `Phone` varchar(50) comment '电话',
 `IsDefault` bool comment '是否为默认地址',
 primary key (AddressId)
);

alter table Address comment '收货地址';

/*==============================================================*/
/* Table: ArticleComment */
/*==============================================================*/
create table ArticleComment
(
 `ArticleCommentId` int not null auto_increment comment '文章评论编号',
 `ArticleId` int not null comment '文章编号',
 `UserId` int not null comment '用户编号',
 `ArticleCommentContent` varchar(4000) not null comment '文章评论内容',
 `ArticleCommentDate` timestamp default CURRENT_TIMESTAMP comment '文章评论时间',
 `ArticleCommentState` int default 1 comment '状态',
 `ArticleRemark` int comment '打分',
 `ArticleCommentReserver1` varchar(4000) comment '备用1',
 `ArticleCommentReserver2` varchar(4000) comment '备用2',
 primary key (ArticleCommentId)
);

alter table ArticleComment comment '文章评论';

/*==============================================================*/
/* Table: ArticleType */
/*==============================================================*/
create table ArticleType
(
 `ArticleTypeId` int not null auto_increment comment '文章栏目编号',
 `ArticleTypeName` varchar(200) comment '文章栏目名称',
 `ArticleTypeState` int default 1 comment '状态',
 `ArticleTypeDesc` varchar(4000) comment '文章栏目描述',
 `ArticleTypePicture` varchar(400) comment '文章栏目图片',
 `ArticleTypeReserve1` varchar(4000) comment '备用1',
 `ArticleTypeReserve2` varchar(4000) comment '备用2',
 primary key (ArticleTypeId)
);

alter table ArticleType comment '文章栏目';

/*==============================================================*/
/* Table: Articles */
/*==============================================================*/
create table Articles
(
 `ArticleId` int not null auto_increment comment '文章编号',
 `ArticleTypeId` int not null comment '文章栏目编号',
 `ArticleTitle` varchar(400) not null comment '文章标题',
 `ArticleContent` text comment '文章内容',
 `ArticleDate` timestamp default CURRENT_TIMESTAMP comment '文章发布时间',
 `ArticleAuthor` varchar(200) comment '文章发布者',
 `ArticleFileName` varchar(100) comment '静态文件名',
 `ArticleThumbNail` varchar(200) comment '缩略图片',
 `ArticleAddition` varchar(200) comment '附件名称',
 `ArticleLevel` int comment '显示的优先级',
 `ArticleIsAllowComment` integer default 1 comment '是否允许评论',
 `ArticleState` int default 1 comment '状态',
 `ArticleHotCount` int comment '点击次数',
 `ArticleReserve1` varchar(4000) comment '备用1',
 `ArticleReserve2` varchar(4000) comment '备用2',
 `ArticleReserve3` numeric(8,0) comment '备用3',
 primary key (ArticleId)
);

alter table Articles comment '文章';

/*==============================================================*/
/* Table: DictSub */
/*==============================================================*/
create table DictSub
(
 `SubId` int not null auto_increment comment '子项编号',
 `DictId` int not null comment '字典编号',
 `SubName` varchar(200) not null comment '子项名称',
 `SubDesc` varchar(4000) comment '子项描述',
 `SubReserve1` varchar(4000) comment '保留备用1',
 primary key (SubId)
);

alter table DictSub comment '字典子项';

/*==============================================================*/
/* Table: DictTop */
/*==============================================================*/
create table DictTop
(
 `DictId` int not null auto_increment comment '字典编号',
 `DictName` varchar(100) not null comment '字典名称',
 `DictDesc` varchar(4000) comment '字典描述',
 `DictReserve1` varchar(4000) comment '保留备用',
 primary key (DictId)
);

alter table DictTop comment '字典';

/*==============================================================*/
/* Table: OrderPdt */
/*==============================================================*/
create table OrderPdt
(
 `OrderPdtId` int not null auto_increment comment '订单商品编号',
 `Id` int not null comment '编号',
 `UserId` int not null comment '用户编号',
 `OrderId` int comment '订单号',
 `PdtAmount` int comment '订购数量',
 `PdtPrice` decimal comment '单价',
 `PdtReserve1` varchar(2000) comment '备用1',
 `PdtReserve2` varchar(4000) comment '备用2',
 primary key (OrderPdtId)
);

alter table OrderPdt comment '订单商品';

/*==============================================================*/
/* Table: Orders */
/*==============================================================*/
create table Orders
(
 `OrderId` int not null auto_increment comment '订单号',
 `AddressId` int not null comment '收货地址编号',
 `OrderState` int default 1 comment '订单状态',
 `ExpressNO` varchar(50) comment '快递编号',
 `ExpressName` varchar(50) comment '快递名称',
 `PayMoney` decimal comment '应支付',
 `PayedMoney` decimal comment '已支付',
 `SendInfo` varchar(300) comment '发货人信息',
 `BuyDate` timestamp default CURRENT_TIMESTAMP comment '下单时间',
 `PayDate` datetime comment '支付时间',
 `SendDate` datetime comment '发货时间',
 `ReceivDate` datetime comment '收货时间',
 `OrderMessage` varchar(4000) comment '附言',
 `UserId` integer comment '用户编号',
 `OrderReserve1` varchar(4000) comment '备用1',
 `OrderReserve2` varchar(4000) comment '备用2',
 `OrderReserve3` decimal comment '备用3',
 primary key (OrderId)
);

alter table Orders comment '订单';

/*==============================================================*/
/* Table: ProductComment */
/*==============================================================*/
create table ProductComment
(
 `ProductCommentId` int not null auto_increment comment '商品评论编号',
 `ProductId` int not null comment '商品编号',
 `UserId` int not null comment '用户编号',
 `ProductCommentContent` varchar(4000) comment '商品评论内容',
 `ProductCommentDate` timestamp default CURRENT_TIMESTAMP comment '商品评论时间',
 `ProductCommentState` int comment '状态',
 `ProductCommentRemark` int comment '打分',
 `ProductCommentReserve1` varchar(4000) comment '备用1',
 `ProductCommentReserve2` varchar(4000) comment '备用2',
 primary key (ProductCommentId)
);

alter table ProductComment comment '商品评论';

/*==============================================================*/
/* Table: Products */
/*==============================================================*/
create table Products
(
 `Id` int not null auto_increment comment '编号',
 `Name` varchar(200) not null comment '名称',
 `SubIdColor` int not null comment '所属颜色',
 `SubIdBrand` int not null comment '所属品牌',
 `SubIdInlay` int not null comment '所属镶嵌',
 `SubIdMoral` int not null comment '所属寓意',
 `SubIdMaterial` int not null comment '所属种水',
 `SubIdTopLevel` int not null comment '一级分类编号',
 `MarketPrice` decimal comment '市场参考价',
 `MyPrice` decimal not null comment '玉源直销价',
 `Discount` decimal default 1 comment '折扣',
 `Picture` varchar(200) comment '图片',
 `Amount` int comment '库存量',
 `Description` text comment '详细描述',
 `State` int default 1 comment '状态',
 `AddDate` timestamp default CURRENT_TIMESTAMP comment '上货日期',
 `Hang` int comment '挂件',
 `RawStone` int comment '赌石',
 `Size` varchar(200) comment '尺寸',
 `ExpressageName` varchar(100) comment '快递名称',
 `Expressage` decimal comment '快递费',
 `AllowComment` int default 1 comment '是否允许评论',
 `Reserve1` varchar(4000) comment '保留备用1',
 `Reserve2` varchar(4000) comment '保留备用2',
 `Reserve3` decimal(0) comment '保留备用3',
 primary key (Id)
);

alter table Products comment '商品';

/*==============================================================*/
/* Table: Users */
/*==============================================================*/
create table Users
(
 `UserId` int not null auto_increment comment '用户编号',
 `UserName` varchar(200) not null comment '用户名',
 `Password` varchar(512) not null comment '密码',
 `Email` varchar(100) not null comment '邮箱',
 `Sex` varchar(10) comment '性别',
 `State` int default 1 comment '状态',
 `RightCode` int comment '权限状态',
 `RegDate` timestamp default CURRENT_TIMESTAMP comment '注册时间',
 `RegIP` varchar(200) comment '注册IP',
 `LastLoginDate` datetime comment '最近登录时间',
 `UserReserve1` varchar(4000) comment '保留备用1',
 `UserReserve2` varchar(4000) comment '保留备用2',
 `UserReserve3` varchar(4000) comment '保留备用3',
 primary key (UserId)
);

alter table Users comment '用户';

alter table Address add constraint FK_AddressBelongUser foreign key (UserId)
 references Users (UserId) on delete restrict on update restrict;

alter table ArticleComment add constraint FK_ArticleCommentForArticle foreign key (ArticleId)
 references Articles (ArticleId) on delete restrict on update restrict;

alter table ArticleComment add constraint FK_ArticleCommentForUser foreign key (UserId)
 references Users (UserId) on delete restrict on update restrict;

alter table Articles add constraint FK_ArticleBelongType foreign key (ArticleTypeId)
 references ArticleType (ArticleTypeId) on delete restrict on update restrict;

alter table DictSub add constraint FK_BelongDict foreign key (DictId)
 references DictTop (DictId) on delete cascade on update cascade;

alter table OrderPdt add constraint FK_BelongOrder foreign key (OrderId)
 references Orders (OrderId) on delete cascade on update cascade;

alter table OrderPdt add constraint FK_CartForUser foreign key (UserId)
 references Users (UserId) on delete restrict on update restrict;

alter table OrderPdt add constraint FK_OrderDepProduct foreign key (Id)
 references Products (Id) on delete restrict on update restrict;

alter table Orders add constraint FK_OrderBelongAddress foreign key (AddressId)
 references Address (AddressId) on delete restrict on update restrict;

alter table ProductComment add constraint FK_ProductCommentBelongUsers foreign key (UserId)
 references Users (UserId) on delete restrict on update restrict;

alter table ProductComment add constraint FK_ProductCommentForProduct foreign key (ProductId)
 references Products (Id) on delete restrict on update restrict;

alter table Products add constraint FK_BelongBrand foreign key (SubIdMaterial)
 references DictSub (SubId) on delete restrict on update restrict;

alter table Products add constraint FK_BelongColor foreign key (SubIdBrand)
 references DictSub (SubId) on delete restrict on update restrict;

alter table Products add constraint FK_BelongInlay foreign key (SubIdInlay)
 references DictSub (SubId) on delete restrict on update restrict;

alter table Products add constraint FK_BelongMaterial foreign key (SubIdColor)
 references DictSub (SubId) on delete restrict on update restrict;

alter table Products add constraint FK_BelongMoral foreign key (SubIdTopLevel)
 references DictSub (SubId) on delete restrict on update restrict;

alter table Products add constraint FK_BelongTopLevel foreign key (SubIdMoral)
 references DictSub (SubId) on delete restrict on update restrict;