Global Platform API
===================

Introduction
------------
ここにGlobal Platform APIの仕様を書きます．

TEE Client API
--------------

TEE Client APIの使用例
^^^^^^^^^^^^^^^^^^^^^^^
::
    TEEC_Result TEEC_InitializeContext(
    const char* name,
    TEEC_Context* context)

    void TEEC_FinalizeContext(
        TEEC_Context* context)

    TEEC_Result TEEC_OpenSession (
        TEEC_Context* context,
        TEEC_Session* session,
        const TEEC_UUID* destination,
        uint32_t connectionMethod,
        const void* connectionData,
        TEEC_Operation* operation,
        uint32_t* returnOrigin)

    void TEEC_CloseSession (
        TEEC_Session* session)

    TEEC_Result TEEC_InvokeCommand(
        TEEC_Session* session,
        uint32_t commandID,
        TEEC_Operation* operation,
        uint32_t* returnOrigin)

TEE Internal Core API
---------------------

