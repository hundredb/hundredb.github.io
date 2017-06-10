title: bug情况
date: 2017-5-31 10:00:00
categories: 
- bug
tags: 
- bug

---

落下的进度


# 待办事项

## 1.`ContactViewController`,出现乱序,换行有误

![详情如下](http://okbqg56m9.bkt.clouddn.com/bug1.gif)

2. 关于约束冲突主要是`hinput的冲突,设置死了固定宽度,这个需要修改`
    关键字`AddEditItem`具体使用的类`ProductChangePlaceOrderManager`

    ```
    #pragma mark - public
-(void)setRightTitle:(NSString *)rightTitle
{
    _rightTitle = rightTitle;
    if (!_rightBtn) {
        UIButton *topBtn = [UIButton new];
        [topBtn setTitle:rightTitle forState:UIControlStateNormal];
        topBtn.titleLabel.font = HTitleFontSize;
        [topBtn setTitleColor:hGBtnYellowTextColor forState:UIControlStateNormal];
        [topBtn setTitleColor:hHighLightTextColor forState:UIControlStateHighlighted];
        topBtn.layer.borderWidth = 1;
        topBtn.layer.borderColor = hGBtnYellowTextColor.CGColor;
        topBtn.layer.cornerRadius = 5;
        topBtn.backgroundColor = [UIColor clearColor];
        [topBtn addTarget:self action:@selector(btnAction) forControlEvents:UIControlEventTouchUpInside];
        [self addSubview:topBtn];
        _rightBtn = topBtn;
    }
    
    WEAK_SELF;
    [_textField mas_remakeConstraints:^(MASConstraintMaker *make) {
        make.left.equalTo(weakSelf);
        make.centerY.equalTo(weakSelf);
        make.top.bottom.equalTo(weakSelf);
        make.width.lessThanOrEqualTo(weakSelf).multipliedBy(0.7);
    }];
    
    [_rightBtn mas_remakeConstraints:^(MASConstraintMaker *make) {
        make.right.equalTo(weakSelf);
        make.centerY.equalTo(weakSelf);
        make.left.equalTo(_textField.mas_right).with.priorityHigh();
        make.height.equalTo(_textField.mas_height);
//        make.width.greaterThanOrEqualTo(weakSelf).multipliedBy(0.3);
    }];
}    
    ```
3. 
# 目前已经修复的






# 其他需要修改的

1. 混淆设计
2. 代码优化





