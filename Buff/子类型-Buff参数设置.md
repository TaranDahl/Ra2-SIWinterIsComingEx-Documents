# 子类型-Buff 参数设置

Buff 拥有众多可以修改（覆盖）的属性，对于弹头或脚本来说，使用一堆属性来覆盖 Buff 本身的属性是不合适的，既不方便编写 ini，也不方便维护，于是便增加了此类型。   
在任意需要挂载、激发、结束、变更、修改 Buff 效果强度值的地方，均可以使用此类型来代替各种参数。



## 注册

位于 `rulesmd.ini`：

```ini
[PackTypes.BuffSetting]
0=BuffSetting1
1=BuffSetting2
2=BuffSetting3
```

### 注意

* 索引从 0 开始。

* 此类型并不需要注册，只是提供了这个功能。



## 完整结构

位于 `rulesmd.ini`：

```ini
[SomeBuffSetting]
; 挂载持续时间
DurationSelf=no                                 ; yes/no , 是否使用 Buff 自身设置的 Duration 而非下方的 Duration 的值 , 默认值是 no
DurationValueType=Normal                        ; 数值类型 , 决定 Duration 属性的具体值 , 默认值是 Normal (不区分大小写)
                                                ; 可用值 : Normal (普通数值) , Global (全局变量) , Local (局部变量) , House (指定的作战方局部变量)
                                                ; 当值为 Global , Local , House 时 , Numbers 中对应的数值会作为索引 (去尾转为整数) 来取出相应的变量的值 , 变量不存在时取出它们的默认值 0
Duration=0                                      ; 整数 , 附加给 Buff 的挂载持续时间 , 0 = 无效果 , 默认值是 0 , 单位 : 帧
                                                ; 当目标单位未持有此 Buff 时 , 此为挂载持续时间 , 负数 = 无限
                                                ; 当目标单位持有此 Buff 时 , 此为增加的挂载持续时间 , 负数 = 倒扣
DurationMax=None                                ; 整数 , 附加挂载持续时间后 , Buff 的最终挂载持续时间的最大值 , None 或 N = 不限制 , 小于 0 按 0 算 , 默认值是 None (不区分大小写) , 单位 : 帧
DurationMin=None                                ; 整数 , 附加挂载持续时间后 , Buff 的最终挂载持续时间的最小值 , None 或 N = 不限制 , 小于 0 按 0 算 , 默认值是 None (不区分大小写) , 单位 : 帧
                                                ; 这里的上下限不会覆盖 Buff 自身设置的上下限 , 它们会一起生效 , Buff 自身设置的上下限优先级更高一点
DurationReset=no                                ; yes/no , 是否使用这里的数值覆盖 Buff 的挂载持续时间 (而不是增减) , 默认值是 no
                                                ; 当 DurationReset=yes 且 Duration < 0 时 , 会把 Buff 的挂载持续时间覆盖成永久
                                                ; 当 DurationReset=yes 且 Duration == 0 时 , 会使用 Buff 自己的默认挂载持续时间
DurationEffect=yes                              ; yes/no , 附加的挂载持续时间是否会受到单位的 Buff 抗性的影响 , 默认值是 yes
DurationAffectAfter=no                          ; yes/no , 是否会给处于【结束状态】的 Buff 增加挂载持续时间 , 默认值是 no

; 生命值
HealthSelf=no                                   ; yes/no , 是否使用 Buff 自身设置的 Health 而非下方的 Health 的值 , 默认值是 no , 单位 : 点
HealthValueType=Normal                          ; 数值类型 , 决定 Health 属性的具体值 , 默认值是 Normal (不区分大小写)
                                                ; 可用值 : Normal (普通数值) , Global (全局变量) , Local (局部变量) , House (指定的作战方局部变量)
                                                ; 当值为 Global , Local , House 时 , Numbers 中对应的数值会作为索引 (去尾转为整数) 来取出相应的变量的值 , 变量不存在时取出它们的默认值 0
Health=0                                        ; 浮点数 , 附加给 Buff 的生命值 , 0 = 无效果 , 默认值是 0
                                                ; 当目标单位未持有此 Buff 时 , 此为生命值 , 负数 = 无敌 , 0 = 一碰就凉
                                                ; 当目标单位持有此 Buff 时 , 此为增加的生命值 , 负数 = 倒扣
HealthMax=None                                  ; 浮点数 , 附加生命值后 , Buff 的最终生命值的最大值 , None 或 N = 不限制 , 小于 0 按 0 算 , 默认值是 None (不区分大小写) , 单位 : 点
HealthMin=None                                  ; 浮点数 , 附加生命值后 , Buff 的最终生命值的最小值 , None 或 N = 不限制 , 小于 0 按 0 算 , 默认值是 None (不区分大小写) , 单位 : 点
                                                ; 这里的上下限不会覆盖 Buff 自身设置的上下限 , 它们会一起生效 , Buff 自身设置的上下限优先级更高一点
HealthReset=no                                  ; yes/no , 是否使用这里的数值覆盖 Buff 的生命值 (而不是增减) , 默认值是 no
                                                ; 当 HealthReset=yes 且 Health < 0 时 , 会把 Buff 的生命值覆盖成无敌
                                                ; 当 HealthReset=yes 且 Health == 0 时 , 会使用 Buff 自己的默认生命值
HealthEffect=yes                                ; yes/no , 附加的生命值是否会受到单位的 Buff 抗性的影响 , 默认值是 yes

; 效果强度值
PowerValueType=Normal                           ; 数值类型 , 决定 Power 属性的具体值 , 默认值是 Normal (不区分大小写)
                                                ; 可用值 : Normal (普通数值) , Global (全局变量) , Local (局部变量) , House (指定的作战方局部变量)
                                                ; 当值为 Global , Local , House 时 , Numbers 中对应的数值会作为索引 (去尾转为整数) 来取出相应的变量的值 , 变量不存在时取出它们的默认值 0
Power=0                                         ; 浮点数 , 附加给 Buff 的效果强度值 , 负数 = 倒扣 , 0 = 无效果 , 默认值是 0 , 单位 : 点
PowerMax=None                                   ; 浮点数 , 附加效果强度值后 , Buff 的最终效果强度值的最大值 , None 或 N = 不限制 , 默认值是 None (不区分大小写) , 单位 : 点
PowerMin=None                                   ; 浮点数 , 附加效果强度值后 , Buff 的最终效果强度值的最小值 , None 或 N = 不限制 , 默认值是 None (不区分大小写) , 单位 : 点
PowerReset=no                                   ; yes/no , 是否使用这里的数值覆盖 Buff 的效果强度值 (而不是增减) , 默认值是 no
PowerEffect=yes                                 ; yes/no , 附加的效果强度值是否会受到单位的 Buff 抗性的影响 , 默认值是 yes
```

### 算法

当 Buff 合并一个【Buff 参数设置】时，Buff 的相关属性会按照如下算法进行加算。  
对于无限（无敌）的 Buff，`Duration` 和 `Health` 不会被合并（包括相关的最大值和最小值），`Power` 等其他属性不受此影响。

```lua
最终属性值 = min( max( 增减后的属性值 , 最小值 ) , 最大值 )
```

### 注意

* 当目标单位未持有此 Buff 时（即挂载 Buff 时），`DurationReset` 和 `PowerReset` 无论取何值都是 **覆盖** 的效果。