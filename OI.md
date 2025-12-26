# OI OS Integration Guide for OI-MARM-Systems

## ✅ **CURRENT STATUS: COMPATIBLE**

**This server now supports STDIO transport and can be installed in OI OS!**

---

## 🎉 Installation

### Prerequisites

- **Python 3.10+** (required)
- **FastMCP** (using OI-OS fork for stability)

### Quick Install

```bash
# Install via OI OS
oi install https://github.com/OI-OS/OI-MARM-Systems.git
```

### Manual Installation

If auto-install fails, connect manually:

```bash
cd MCP-servers/OI-MARM-Systems/marm-mcp-server
pip install -r requirements_stdio.txt  # Install STDIO dependencies
cd ../../..  # Back to OI OS root
./oi connect OI-MARM-Systems python3 "MCP-servers/OI-MARM-Systems/marm-mcp-server/server_stdio.py"
```

### What Changed

- ✅ **STDIO Support:** New `server_stdio.py` using FastMCP (OI-OS fork)
- ✅ **All 19 Tools:** All tools converted from FastAPI routes to FastMCP tools
- ✅ **Core Logic Reused:** All business logic preserved from original server
- ✅ **No FastAPI Dependency:** Removed FastAPI/uvicorn for STDIO compatibility

### Installation Note

**Current Status:** The `oi install` command will clone the repository and apply intent mappings, but may require manual connection step due to server command auto-detection limitations. If install fails at connection, use the manual connection steps below.

---

## 📋 Server Information

### What is OI-MARM-Systems?

**MARM (Memory Accurate Response Mode)** is a universal MCP server providing intelligent memory that saves across sessions for AI conversations with:

- **Semantic Search** - Find memories by meaning, not keywords
- **Cross-App Memory** - Share memories between AI clients (Claude, Qwen, Gemini)
- **Auto-Classification** - Content automatically categorized for intelligent recall
- **Session Management** - Organize conversations with structured logging

### Available Tools (19 Total)

| Category | Tools |
|----------|-------|
| **Session** | `marm_start`, `marm_refresh` |
| **Memory** | `marm_smart_recall`, `marm_contextual_log` |
| **Logging** | `marm_log_session`, `marm_log_entry`, `marm_log_show`, `marm_log_delete` |
| **Notebook** | `marm_notebook_add`, `marm_notebook_use`, `marm_notebook_show`, `marm_notebook_status`, `marm_notebook_clear`, `marm_notebook_delete` |
| **Workflow** | `marm_summary`, `marm_context_bridge` |
| **System** | `marm_current_context`, `marm_system_info`, `marm_reload_docs` |

**Note:** All 19 tools have been tested and verified 100% functional via direct calls.

### Version

- **Current Version:** 2.2.6
- **Repository:** https://github.com/OI-OS/OI-MARM-Systems
- **Original Repository:** https://github.com/Lyellr88/MARM-Systems

---

## 📋 Server Files

### STDIO Server (Recommended for OI OS)

- **File:** `marm-mcp-server/server_stdio.py`
- **Dependencies:** `requirements_stdio.txt`
- **Transport:** STDIO (compatible with OI OS)
- **Tools:** All 19 tools available

### HTTP Server (Original)

- **File:** `marm-mcp-server/server.py`
- **Dependencies:** `requirements.txt`
- **Transport:** HTTP/WebSocket (for other MCP clients)
- **Use Case:** Docker deployment, Claude Desktop with HTTP transport

---

## 🔧 Integration Steps

### Step 1: Install Dependencies

```bash
cd MCP-servers/OI-MARM-Systems/marm-mcp-server
pip install -r requirements_stdio.txt
```

### Step 2: Connect Server

```bash
# From OI OS root directory
./oi connect OI-MARM-Systems python3 "MCP-servers/OI-MARM-Systems/marm-mcp-server/server_stdio.py"
```

### Step 3: Verify Connection

```bash
./oi status OI-MARM-Systems
./oi tools OI-MARM-Systems  # Should show all 19 tools
```

### Step 4: Test a Tool

```bash
./oi call OI-MARM-Systems marm_system_info
```

---

## ✅ Current Status

### Working Features

1. ✅ **STDIO Transport** - Fully compatible with OI OS
2. ✅ **All 19 Tools** - All tools converted, tested, and verified 100% functional
3. ✅ **Core Logic** - All business logic preserved
4. ✅ **Semantic Search** - Full semantic search support with similarity scores
5. ✅ **Session Management** - Complete session handling (create, switch, bridge, delete)
6. ✅ **Memory System** - Full memory storage and recall with auto-classification
7. ✅ **Intent Mappings** - 53 natural language keywords configured
8. ✅ **Parameter Extractors** - 32 parameter extraction rules added

### Testing Status

**✅ All 19 Tools Tested and Verified:**
- Direct tool calls: 100% success rate
- Semantic search: Working with cross-session support
- Session operations: All CRUD operations verified
- Notebook system: Full lifecycle tested (add, use, show, status, clear, delete)
- Context bridging: Verified between sessions
- Memory operations: Storage, recall, and deletion all working

**Note:** Natural language parameter extraction has known limitations (same as other servers). Use direct calls for reliable results.

---

## 📚 Documentation

### Official Documentation

- **MCP Handbook:** `MCP-HANDBOOK.md` - Complete usage guide with all 19 tools
- **MARM Handbook:** `MARM-HANDBOOK.md` - Original MARM protocol handbook
- **Protocol:** `PROTOCOL.md` - Quick start commands and protocol reference
- **Installation Guides:**
  - `docs/INSTALL-DOCKER.md` - Docker deployment
  - `docs/INSTALL-LINUX.md` - Linux installation
  - `docs/INSTALL-WINDOWS.md` - Windows installation

### External Resources

- **GitHub Repository:** https://github.com/OI-OS/OI-MARM-Systems
- **Original Repository:** https://github.com/Lyellr88/MARM-Systems
- **MCP Protocol:** https://modelcontextprotocol.org
- **MARM Systems:** https://marmsystems.com

---

## ✅ Verification

**Current Status:** ✅ **FULLY COMPATIBLE**

To verify installation:

```bash
# Check Python version
python3 --version  # Should be 3.10+

# Check server connection
./oi status OI-MARM-Systems

# List all tools
./oi tools OI-MARM-Systems  # Should show 19 tools

# Test a tool
./oi call OI-MARM-Systems marm_system_info
```

---

## 🎯 Summary

**OI-MARM-Systems is now fully compatible with OI OS!**

✅ **STDIO Support:** New `server_stdio.py` using FastMCP
✅ **All Tools Working:** All 19 tools converted, tested, and verified 100% functional
✅ **Python 3.10+:** Required and available
✅ **Core Logic Preserved:** All business logic reused from original
✅ **Intent Mappings:** 53 natural language keywords configured
✅ **Parameter Extractors:** 32 extraction rules added

**Installation:**
```bash
oi install https://github.com/OI-OS/OI-MARM-Systems.git
```

**Manual Connection:**
```bash
./oi connect OI-MARM-Systems python3 "MCP-servers/OI-MARM-Systems/marm-mcp-server/server_stdio.py"
```

---

## 📝 Installation Notes

See `INSTALLATION_NOTES.md` for detailed technical information about the incompatibility issues.

