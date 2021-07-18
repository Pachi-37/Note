[返回](../Mermaid.md)

# StateDiagram



### 状态

`stateDiagram-v2`

`[stateName]` 或 `state ["stateName"] as [name]` 或 `[stateName]:[context]`



```mermaid
stateDiagram
id
state "tmp" as i
test:This is test
```



### 转移

`[state] --> [state]:[Note]`



### 开始和结束标志	

`[*]`



### 复合状态

`state [stateName]{[body]}`



### 分支与汇合

`<<fork>>` `<<join>>`

```mermaid
stateDiagram
state fork_state <<fork>>
[*] --> fork_state

state join_state <<join>>

fork_state --> join_state
```



### 提示

`note [right] of [stateName]`

`statement`

`end note`





### 并发性

`--`

```mermaid
stateDiagram-v2
    [*] --> Active

    state Active {
        [*] --> NumLockOff
        NumLockOff --> NumLockOn : EvNumLockPressed
        NumLockOn --> NumLockOff : EvNumLockPressed
        --
        [*] --> CapsLockOff
        CapsLockOff --> CapsLockOn : EvCapsLockPressed
        CapsLockOn --> CapsLockOff : EvCapsLockPressed
        --
        [*] --> ScrollLockOff
        ScrollLockOff --> ScrollLockOn : EvScrollLockPressed
        ScrollLockOn --> ScrollLockOff : EvScrollLockPressed
    }
```

