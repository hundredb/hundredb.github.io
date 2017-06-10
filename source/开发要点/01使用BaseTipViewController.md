title: 01使用BaseTipViewController
date: 2017-6-2 10:00:00
categories: 
- 组件使用
tags: 
- 组件使用

---

01使用BaseTipViewController

# 前言

关于01使用BaseTipViewController的使用方法

参考类: `ProductChangeSuccessViewController`


# 核心代码


```
-(TipViewModel *)mockModel
{
    if (!_mockModel) {
        
        NSMutableAttributedString *title = [[NSMutableAttributedString alloc] initWithString:@"订单可点击订单详情或在首页进入我的订单进行查看"];
        NSRange titleRange = {5,4};
        [title addAttribute:NSUnderlineStyleAttributeName value:[NSNumber numberWithInteger:NSUnderlineStyleSingle] range:titleRange];
        [title addAttribute:NSForegroundColorAttributeName value:hBlueTextColor range:NSMakeRange(5,4)];
        NSDictionary *dic = @{
                              @"title":@"恭喜您!产品转换成功 ",
                              @"detail":@"请尽快补充相关资料",
                              @"functionStr":@"意向书电子签名",
                              @"detailBtnStr":title,
                              @"style":@0,
                              };
        
        TipViewModel *model = [TipViewModel mj_objectWithKeyValues:dic];
        _mockModel = model;
    }
    
    return _mockModel;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    self.navTitleLabel.text = @"下单完成";
    self.originModel = self.mockModel;
}
```


# 例子全代码


```
#import "ProductChangeSuccessViewController.h"

#import "OrderDetialViewController.h"   //参考借鉴

#import "ProductChangeOrderDetailViewController.h"
#import "SupplementViewController.h"
#import "SignViewController.h"


@interface ProductChangeSuccessViewController ()

@property(nonatomic,strong)TipViewModel *mockModel;

@end

@implementation ProductChangeSuccessViewController

#pragma mark - public

//详情按钮操作
- (void)orderDetailBtnAction
{
    OrderDetialViewController *vc = [OrderDetialViewController new];
    vc.orderNo = @"T0258820170602006159";
//    vc.orderNo = self.orderNo;
    [self.navigationController pushViewController:vc animated:YES];
    
}

//影像操作
- (void)updatePhotoBtnAction
{
    SupplementViewController *vc = [SupplementViewController new];
    [self.navigationController pushViewController:vc animated:YES];
}

//功能键操作
- (void)functionBtnAction
{
    SignViewController *vc = [SignViewController new];
    [self.navigationController pushViewController:vc animated:YES];
}



#pragma mark - private
-(void)onBackButtonClick
{
    [self.navigationController popToRootViewControllerAnimated:YES];
}

-(TipViewModel *)mockModel
{
    if (!_mockModel) {
        
        NSMutableAttributedString *title = [[NSMutableAttributedString alloc] initWithString:@"订单可点击订单详情或在首页进入我的订单进行查看"];
        NSRange titleRange = {5,4};
        [title addAttribute:NSUnderlineStyleAttributeName value:[NSNumber numberWithInteger:NSUnderlineStyleSingle] range:titleRange];
        [title addAttribute:NSForegroundColorAttributeName value:hBlueTextColor range:NSMakeRange(5,4)];
        NSDictionary *dic = @{
                              @"title":@"恭喜您!产品转换成功 ",
                              @"detail":@"请尽快补充相关资料",
                              @"functionStr":@"意向书电子签名",
                              @"detailBtnStr":title,
                              @"style":@0,
                              };
        
        TipViewModel *model = [TipViewModel mj_objectWithKeyValues:dic];
        _mockModel = model;
    }
    
    return _mockModel;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    self.navTitleLabel.text = @"下单完成";
    self.originModel = self.mockModel;
}



@end

```

