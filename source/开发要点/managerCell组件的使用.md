title: managerCell组件的使用
date: 2017-5-31 10:00:00
categories: 
- 组件使用
tags: 
- 组件使用

---

managerCell组件的使用

# 前言
关于managerCell的使用

请参考`ApprovalTableVC`的使用方法,
或者看例子:`EXTableVC`
![table的例子](http://okbqg56m9.bkt.clouddn.com/Snip20170531_3.png)
![cell父类的方法](http://okbqg56m9.bkt.clouddn.com/Snip20170531_4.png)


# 常规使用方法
![]()

具体代码示例

```
#import "ApprovalTableVC.h"
#import "BaseManagerViewItem.h"
#import "ToDoTableCell.h"

@interface ApprovalTableVC () <UITableViewDelegate,UITableViewDataSource,BaseManagerCellDataSource,BaseManagerViewItemDelegate>


@property (nonatomic, strong) NSArray *data;

@end

@implementation ApprovalTableVC
{
    UITableView *_tableV;
}
- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self _initUI];

}


-(void)_initUI
{
    UITableView *tableV = [UITableView new];
    tableV.delegate = self;
    tableV.dataSource = self;
    tableV.estimatedRowHeight = 580.0f;
    tableV.showsVerticalScrollIndicator = NO;
    tableV.showsHorizontalScrollIndicator = NO;
    tableV.separatorStyle = NO;   //去除分割线
    tableV.backgroundColor = [UIColor clearColor];
    [tableV registerClass:NSClassFromString(@"ToDoTableCell") forCellReuseIdentifier:@"ToDoTableCell"];
    ;
    
    [self.view addSubview:tableV];
    _tableV = tableV;
    WEAK_SELF;
    [tableV mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.equalTo(weakSelf.view);
    }];
    
}

#pragma mark - datasource
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return self.data.count;
}


-(CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath
{
    ToDoTableCell *cell = [tableView dequeueReusableCellWithIdentifier:@"ToDoTableCell"];
    cell.datasource = self;
    cell.dataArr = self.data[indexPath.row];
    [cell.contentView setNeedsLayout];
    [cell.contentView layoutIfNeeded];
    CGSize size = [cell.contentView systemLayoutSizeFittingSize:UILayoutFittingCompressedSize];
    
    
    return [cell totalHeight];
    
    //    return 100;
}

-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    ToDoTableCell *cell = [tableView dequeueReusableCellWithIdentifier:@"ToDoTableCell"];
    cell.backgroundColor = [UIColor clearColor];
    cell.datasource = self;
    cell.dataArr = self.data[indexPath.row];
    
    return cell;
}

-(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
    [tableView deselectRowAtIndexPath:indexPath animated:YES];
    if (self.delegate&&[self.delegate respondsToSelector:@selector(didSelectRowAtIndexPath:)]) {
        [self.delegate didSelectRowAtIndexPath:indexPath.row];
    }
}


#pragma mark - cellDatasource,主要是创建第一个数据
-(NSArray<BaseManagerOriginModel *> *)originalDatasourceWithCell:(BaseManagerCell *)cell
{
    NSArray *arr =@[
                    @{@"style":@0,@"title":@"客户",@"key":@"name"},
                    @{@"style":@0,@"title":@"产品名称",@"key":@"product"},
                    @{@"style":@0,@"title":@"理财经理",@"key":@"rm"},
                    ];
    
    NSMutableArray *tmpArr = [@[] mutableCopy];
    for (NSDictionary *dic in arr) {
        BaseManagerOriginModel *model = [BaseManagerOriginModel mj_objectWithKeyValues:dic];
        [tmpArr addObject:model];
    }
    
    return tmpArr;
}

- (NSArray *)data
{
    if (!_data)
    {
        NSArray * arrData = @[
                              @[@{@"detail" : @"李伯斌", @"key" : @"name"},
                                @{@"detail": @"前海实际基金-宝盈2号B类收益权",@"key" : @"product"},
                                @{@"detail" : @"刘涛(liutao002)",@"key"  :@"rm"}
                                ],
                              
                              @[@{@"detail" : @"李伯斌", @"key" : @"name"},
                                @{@"detail": @"前海实际基金-宝盈2号B类收益权",@"key" : @"product"},
                                @{@"detail" : @"刘涛(liutao002)",@"key"  :@"rm"}
                                ],
                              
                              @[@{@"detail" : @"李伯斌", @"key" : @"name"},
                                @{@"detail": @"前海实际基金-宝盈2号B类收益权",@"key" : @"product"},
                                @{@"detail" : @"刘涛(liutao002)",@"key"  :@"rm"}
                                ]];
        NSMutableArray *mutableArr = [@[] mutableCopy];
        
        for (NSArray *data in arrData)
        {
            NSMutableArray *modelArr = [@[] mutableCopy];
            for (NSDictionary *dic in data)
            {
                [modelArr addObject:[BaseManagerModel mj_objectWithKeyValues:dic]];
            }
            [mutableArr addObject:modelArr];
        }
        _data = mutableArr;
    }
    
    return _data;
}

#pragma mark - 按钮点击事件
-(void)touchOnClickWithBtn:(BaseManagerViewItem *)targetView andData:(NSArray<BaseManagerModel *> *)dataArr
{
    NSLog(@"点击事件,获取点击传值:%@",dataArr);
}


@end


```



# 数据传入修改数据


数据解析

```

- (NSArray *)data
{
    if (!_data)
    {
        NSArray * arrData = @[
                              @[@{@"detail" : @"李伯斌", @"key" : @"name"},
                                @{@"detail": @"前海实际基金-宝盈2号B类收益权",@"key" : @"product"},
                                @{@"detail" : @"刘涛(liutao002)",@"key"  :@"rm"}
                                ],
                              
                              @[@{@"detail" : @"李伯斌", @"key" : @"name"},
                                @{@"detail": @"前海实际基金-宝盈2号B类收益权",@"key" : @"product"},
                                @{@"detail" : @"刘涛(liutao002)",@"key"  :@"rm"}
                                ],
                              
                              @[@{@"detail" : @"李伯斌", @"key" : @"name"},
                                @{@"detail": @"前海实际基金-宝盈2号B类收益权",@"key" : @"product"},
                                @{@"detail" : @"刘涛(liutao002)",@"key"  :@"rm"}
                                ]];
        NSMutableArray *mutableArr = [@[] mutableCopy];
        
        for (NSArray *data in arrData)
        {
            NSMutableArray *modelArr = [@[] mutableCopy];
            for (NSDictionary *dic in data)
            {
                [modelArr addObject:[BaseManagerModel mj_objectWithKeyValues:dic]];
            }
            [mutableArr addObject:modelArr];
        }
        _data = mutableArr;
    }
    
    return _data;
}


```




