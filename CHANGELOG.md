# 更新记录

## 改名说明（2026-11-23）

本插件原名为 `dsh-continue-button`，现改为 **`dsh-editable-send`**。

原因：npm 与 DSH 社区插件目录里已存在另一个同名的 `dsh-continue-button`
（`MrGnUm/dsh-continue-button`，固定 `continue` 提示词、只在轮次停止时出现），
与本插件（文本可编辑、随时可点）是两个不同的东西。为了两个插件都能被准确找到，
本插件改用能表达差异的名字。

**已经装了旧包怎么办**

```powershell
# 1) 卸掉旧的
plugin_manager remove_bundle --target dsh-continue-button

# 2) 装新的
plugin_manager install_bundle --target dsh-editable-send
```

旧的 npm 包已标记为 deprecated，指向新包。旧版存在浏览器里的文本
（`localStorage['dsh-continue-button:text']`）不会自动迁移，新包默认回到「继续」。

## 1.0.0 — 2026-10-29

首个公开版本。

- 输入框右下工具行、官方发送按钮左边多一个按钮，文本默认「继续」（英文界面默认 `Continue`）。
- 左键点按钮 = 把按钮上的文本当成一条普通提问发出去，走官方 `inputActions`（`setDraft` → `submit`），
  和按发送键同一条路：运行中排队、本地回显、失败恢复都由宿主自己管。
- 按钮右侧一个铅笔，点开就地改文本：回车/失焦保存，Esc 放弃，存在浏览器 `localStorage`。
- 草稿保护：发完把用户原本的草稿还回输入框；发送/裁决/命令态下按钮禁用。
- 挂在 `conversation.input.right`（可增 list 槽位，`replaceRisk: none`），不覆盖任何官方控件。
- 渲染外包一层 error boundary：按钮抛错时只消失，不连累输入框那一排。