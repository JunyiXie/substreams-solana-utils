# Substreams Solana 工具库

这是一个专为开发 Solana substreams 而设计的 Rust 工具库，提供了丰富的实用功能来简化 Solana 区块链数据的处理和分析。

## 🚀 功能特性

### 核心功能模块

- **交易处理 (Transaction)**: 提供 Solana 交易的解析、上下文构建和签名验证功能
- **指令处理 (Instruction)**: 支持结构化指令解析，包括内部指令和日志关联
- **账户管理 (Account)**: 账户余额跟踪和状态管理
- **日志分析 (Log)**: 交易日志的解析和结构化处理
- **公钥工具 (Pubkey)**: Solana 公钥的操作和转换工具
- **错误处理 (Error)**: 统一的错误处理机制

### 专用程序支持

- **SPL Token 程序**: 完整的 SPL Token 指令解析和账户状态跟踪
- **System 程序**: 系统程序指令的处理支持

## 📦 安装

在你的 `Cargo.toml` 文件中添加以下依赖：

```toml
[dependencies]
substreams-solana-utils = { git = "https://github.com/0xpapercut/substreams-solana-utils", tag = "v2.0.5" }
```

## 🛠️ 核心依赖

- `substreams`: Substreams 核心框架 (^0.5.0)
- `substreams-solana`: Solana 专用的 substreams 扩展
- `bs58`: Base58 编码解码
- `regex`: 正则表达式支持
- `base64`: Base64 编码解码
- `borsh`: Borsh 序列化格式支持
- `anyhow`: 错误处理

## 📋 主要功能模块详解

### 1. 交易上下文 (TransactionContext)

提供交易处理所需的完整上下文信息：

```rust
pub struct TransactionContext<'a> {
    pub accounts: Vec<PubkeyRef<'a>>,           // 交易涉及的所有账户
    pub account_balances: Vec<AccountBalance>,   // 账户余额变化
    pub token_accounts: HashMap<PubkeyRef<'a>, TokenAccount<'a>>, // Token 账户映射
    pub signers: Vec<PubkeyRef<'a>>,            // 签名者列表
    pub signature: String,                       // 交易签名
}
```

### 2. 结构化指令 (StructuredInstruction)

支持多层级指令处理：
- 编译指令 (Compiled Instructions)
- 内部指令 (Inner Instructions)  
- 指令层级关系追踪
- 日志与指令的关联

### 3. SPL Token 支持

完整的 SPL Token 程序指令解析：
- InitializeAccount/InitializeAccount2/InitializeAccount3
- Transfer/TransferChecked
- MintTo/MintToChecked
- Burn/BurnChecked
- SyncNative
- CloseAccount

### 4. 日志处理

智能日志栈管理：
- 自动关联指令与日志
- 处理截断日志
- 支持嵌套指令的日志分组

## 💡 示例用法

项目包含完整的示例代码，位于 `examples/` 目录：

### 运行示例

1. 设置环境变量 `STREAMINGFAST_KEY`，获取 API key：[StreamingFast Keys](https://app.streamingfast.io/keys)

2. 运行 token 设置脚本：
   ```bash
   . ./token.sh
   ```

3. 启动数据流处理：
   ```bash
   make stream <module_name> START=<slot_number>
   ```

   例如，运行指令日志模块：
   ```bash
   make stream instruction_logs START=293932407
   ```

### 可用示例模块

- **instruction_logs**: 按指令基础读取交易日志的演示

## 🏗️ 项目结构

```
substreams-solana-utils/
├── src/
│   ├── lib.rs              # 主模块入口
│   ├── transaction.rs      # 交易处理功能
│   ├── instruction.rs      # 指令处理功能
│   ├── account.rs          # 账户相关功能
│   ├── log.rs             # 日志处理功能
│   ├── pubkey.rs          # 公钥工具
│   ├── error.rs           # 错误处理
│   ├── spl_token/         # SPL Token 程序支持
│   │   ├── mod.rs
│   │   ├── constants.rs
│   │   ├── instruction.rs
│   │   └── account.rs
│   └── system_program/    # System 程序支持
│       ├── mod.rs
│       ├── constants.rs
│       └── instruction.rs
├── examples/              # 示例代码
│   ├── src/
│   ├── proto/
│   ├── substreams.yaml   # Substreams 配置
│   ├── Makefile          # 构建脚本
│   └── README.md         # 示例说明
├── Cargo.toml            # 项目配置
├── LICENSE               # MIT 许可证
└── README.md            # 项目说明
```

## 🔧 开发环境

### 系统要求

- Rust 1.70+ (2021 Edition)
- WASM 目标支持：`wasm32-unknown-unknown`

### 构建项目

```bash
# 构建库
cargo build

# 构建示例 (WASM)
cd examples
make build
```

## 📝 许可证

本项目使用 MIT 许可证。详情请参见 [LICENSE](LICENSE) 文件。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📚 相关资源

- [Substreams 文档](https://substreams.streamingfast.io/)
- [Solana 开发文档](https://docs.solana.com/)
- [StreamingFast 平台](https://app.streamingfast.io/)
- [Solana Explorer](https://explorer.solana.com/)

## 版本信息

当前版本：v2.0.5

本工具库由 [0xpapercut](https://github.com/0xpapercut) 开发维护。
