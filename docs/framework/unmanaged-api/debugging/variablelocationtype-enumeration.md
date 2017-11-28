---
title: "VariableLocationType 枚举"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
api_name: VariableLocationType
api_location: mscordbi.dll
api_type: COM
f1_keywords: VariableLocationType
helpviewer_keywords: VariableLocationType enumeration [.NET Framework debugging]
ms.assetid: 8635ee3a-c84b-4626-876c-416bee54f787
topic_type: apiref
caps.latest.revision: "5"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 0338a89acdd9c29370bc8e52ed9a099e9330c2cc
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="variablelocationtype-enumeration"></a><span data-ttu-id="9cca6-102">VariableLocationType 枚举</span><span class="sxs-lookup"><span data-stu-id="9cca6-102">VariableLocationType Enumeration</span></span>
<span data-ttu-id="9cca6-103">指示变量的本机位置类型。</span><span class="sxs-lookup"><span data-stu-id="9cca6-103">Indicates the native location type of a variable.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9cca6-104">语法</span><span class="sxs-lookup"><span data-stu-id="9cca6-104">Syntax</span></span>  
  
```  
typedef enum VariableLocationType  
{  
    VLT_REGISTER,               
    VLT_REGISTER_RELATIVE,      
    VLT_INVALID  
} VariableLocationType;  
```  
  
## <a name="members"></a><span data-ttu-id="9cca6-105">成员</span><span class="sxs-lookup"><span data-stu-id="9cca6-105">Members</span></span>  
  
|<span data-ttu-id="9cca6-106">成员</span><span class="sxs-lookup"><span data-stu-id="9cca6-106">Member</span></span>|<span data-ttu-id="9cca6-107">描述</span><span class="sxs-lookup"><span data-stu-id="9cca6-107">Description</span></span>|  
|------------|-----------------|  
|`VLT_REGISTER`|<span data-ttu-id="9cca6-108">该变量是在寄存器中。</span><span class="sxs-lookup"><span data-stu-id="9cca6-108">The variable is in a register.</span></span>|  
|`VLT_REGISTER_RELATIVE`|<span data-ttu-id="9cca6-109">该变量是在注册相对内存位置。</span><span class="sxs-lookup"><span data-stu-id="9cca6-109">The variable is in a register-relative memory location.</span></span>|  
|`VLT_INVALID`|<span data-ttu-id="9cca6-110">该变量不存储在注册或注册相对内存位置。</span><span class="sxs-lookup"><span data-stu-id="9cca6-110">The variable is not stored in a register or a register-relative memory location.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9cca6-111">备注</span><span class="sxs-lookup"><span data-stu-id="9cca6-111">Remarks</span></span>  
 <span data-ttu-id="9cca6-112">成员`VariableLocationType`枚举返回的[ICorDebugVariableHome::GetLocationType](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-getlocationtype-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="9cca6-112">A member of the `VariableLocationType` enumeration is returned by the [ICorDebugVariableHome::GetLocationType](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-getlocationtype-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9cca6-113">要求</span><span class="sxs-lookup"><span data-stu-id="9cca6-113">Requirements</span></span>  
 <span data-ttu-id="9cca6-114">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="9cca6-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9cca6-115">**标头：** CorDebug.idl、 CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="9cca6-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="9cca6-116">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="9cca6-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="9cca6-117">**.NET framework 版本：**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9cca6-117">**.NET Framework Versions:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9cca6-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="9cca6-118">See Also</span></span>  
 [<span data-ttu-id="9cca6-119">调试枚举</span><span class="sxs-lookup"><span data-stu-id="9cca6-119">Debugging Enumerations</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)