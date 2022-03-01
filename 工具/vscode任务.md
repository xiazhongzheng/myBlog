```
{
  "version": "2.0.0",
  "tasks": [ // 设置快捷键（ctrl+K+S），ctrl+alt+R打开运行任务弹窗
    {
      // 任务的名称
      "label": "git-fetch",
      // 任务类别，shell代表脚本
      "type": "shell",
      // 任务脚本，可以是yarn/npm/git 等
      "command": "git",
      // 命令参数
      "args": [
        "fetch"
      ],
      // 声明无需扫描脚本输出
      "problemMatcher": []
    },
    {
      "label": "git-pull",
      "type": "shell",
      "command": "git",
      "args": [
        "pull",
      ],
      "group": "build",
      "problemMatcher": []
    },
    { // 输入参数
      "label": "git-checkout-b",
      "type": "shell",
      "command": "git",
      "args": [
        "checkout",
        "-b",
        "${input:branchName}", // 变量，会在下面的inputs中搜寻名叫branch的id
        "origin/${input:branchName}"
      ],
      "group": "build",
      "problemMatcher": []
    },
    { // 输入参数
      "label": "git-checkout",
      "type": "shell",
      "command": "git",
      "args": [
        "checkout",
        "${input:branchName}"
      ],
      "group": "build",
      "problemMatcher": []
    },
    { // 执行任务链
      "label": "git-checkout-pull",
      "type": "shell",
      "dependsOn": [ // 依赖的任务
          "git-checkout",
          "git-pull"
      ],
      "dependsOrder": "sequence", // 代表是依次执行，不设置会并行执行
      "problemMatcher": []
    }
  ],
  "inputs": [
    {
      "id": "branch", // 输入参数的id，与上面变量${input:branch}这个branch保持一致
      "type": "pickString",
      "options": [
        "dev",
        "feature-20211220-68043-tmsPayCheck"
      ],
      "description": "请输入分支"
    },
    {
      "type": "promptString",
      "id": "branchName",
      "description": "input your branch name",
      "default": "release"
    }
  ],
}
```