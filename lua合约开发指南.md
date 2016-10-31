**<span style="background: #f8fafe">lua</span>**<span
lang="zh-CN">**<span
style="background: #f8fafe">合约开发指南</span>**</span>


##<span lang="zh-CN">目录</span>

[1<span
lang="zh-CN">注意事项</span>](#__RefHeading__1736_1702457476)[2](#__RefHeading__1736_1702457476)

[1.1<span
lang="zh-CN">由于安全性考虑，合约中只能使用</span>](#__RefHeading__1738_1702457476)[lua<span
lang="zh-CN">中</span>](#__RefHeading__1738_1702457476)[table<span
lang="zh-CN">，</span>](#__RefHeading__1738_1702457476)[math<span
lang="zh-CN">，</span>](#__RefHeading__1738_1702457476)[string<span
lang="zh-CN">库，不能使用</span>](#__RefHeading__1738_1702457476)[io<span
lang="zh-CN">操作等。</span>](#__RefHeading__1738_1702457476)[2](#__RefHeading__1738_1702457476)

[1.2<span
lang="zh-CN">脚本现在只能写在一个文件中，不支持多文件。</span>](#__RefHeading__1740_1702457476)[2](#__RefHeading__1740_1702457476)

[1.3<span
lang="zh-CN">脚本大小不能超过</span>](#__RefHeading__1742_1702457476)[64k<span
lang="zh-CN">。</span>](#__RefHeading__1742_1702457476)[2](#__RefHeading__1742_1702457476)

[1.4<span
lang="zh-CN">合约内容通过全局变量“</span>](#__RefHeading__1744_1702457476)[contract”<span
lang="zh-CN">传给脚本，脚本里面可以拿来就用</span>](#__RefHeading__1744_1702457476)[2](#__RefHeading__1744_1702457476)

[1.5<span
lang="zh-CN">账户平衡检测开关通过在</span>](#__RefHeading__1746_1702457476)[lua<span
lang="zh-CN">脚本中的全局变量“</span>](#__RefHeading__1746_1702457476)[gCheckAccount”<span
lang="zh-CN">控制，默认关闭此开关。</span>](#__RefHeading__1746_1702457476)[2](#__RefHeading__1746_1702457476)

[1.6<span
lang="zh-CN">合约内容不能超过</span>](#__RefHeading__1748_1702457476)[4096<span
lang="zh-CN">字节。</span>](#__RefHeading__1748_1702457476)[2](#__RefHeading__1748_1702457476)

[1.7<span
lang="zh-CN">脚本中如果有异常，或逻辑不对，可以通过</span>](#__RefHeading__1750_1702457476)[assert<span
lang="zh-CN">，</span>](#__RefHeading__1750_1702457476)[error<span
lang="zh-CN">退出执行，</span>](#__RefHeading__1750_1702457476)[lua<span
lang="zh-CN">解释器会捕获到该异常。</span>](#__RefHeading__1750_1702457476)[2](#__RefHeading__1750_1702457476)

[1.8<span
lang="zh-CN">脚本中必须以</span>](#__RefHeading__1752_1702457476)[mylib
= require "mylib"<span
lang="zh-CN">开头，通过</span>](#__RefHeading__1752_1702457476)[mylib<span
lang="zh-CN">调用里面的</span>](#__RefHeading__1752_1702457476)[API<span
lang="zh-CN">。</span>](#__RefHeading__1752_1702457476)[2](#__RefHeading__1752_1702457476)

[2<span lang="zh-CN">示例
（充值和提现操作）</span>](#__RefHeading__1754_1702457476)[2](#__RefHeading__1754_1702457476)

[3<span
lang="zh-CN">脚本调试</span>](#__RefHeading__1756_1702457476)[10](#__RefHeading__1756_1702457476)

[3.1 <span
lang="zh-CN">启动</span>](#__RefHeading__1758_1702457476)[dacrs<span
lang="zh-CN">程序</span>](#__RefHeading__1758_1702457476)[10](#__RefHeading__1758_1702457476)

[3.2 <span
lang="zh-CN">导入私钥</span>](#__RefHeading__1760_1702457476)[11](#__RefHeading__1760_1702457476)

[3.3 <span
lang="zh-CN">生成几个测试地址，并充值激活</span>](#__RefHeading__1762_1702457476)[11](#__RefHeading__1762_1702457476)

[3.4 <span
lang="zh-CN">注册应用脚本</span>](#__RefHeading__1764_1702457476)[13](#__RefHeading__1764_1702457476)

[3.5 <span
lang="zh-CN">充值操作</span>](#__RefHeading__1766_1702457476)[13](#__RefHeading__1766_1702457476)

[3.6 <span
lang="zh-CN">提现操作</span>](#__RefHeading__1768_1702457476)[16](#__RefHeading__1768_1702457476)

[3.6.1](#__RefHeading__1770_1702457476)<span
lang="zh-CN">[查看](#__RefHeading__1770_1702457476)</span>[dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6](#__RefHeading__1770_1702457476)<span
lang="zh-CN">[当前余额
：](#__RefHeading__1770_1702457476)</span>[17](#__RefHeading__1770_1702457476)

[3.6.2](#__RefHeading__1772_1702457476)<span
lang="zh-CN">[提现](#__RefHeading__1772_1702457476)</span>[17](#__RefHeading__1772_1702457476)

[3.6.3](#__RefHeading__1774_1702457476)<span
lang="zh-CN">[再次查看](#__RefHeading__1774_1702457476)</span>[dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6](#__RefHeading__1774_1702457476)<span
lang="zh-CN">[当前余额
，发现已经提现了](#__RefHeading__1774_1702457476)</span>[5](#__RefHeading__1774_1702457476)<span
lang="zh-CN">[个币。](#__RefHeading__1774_1702457476)</span>[17](#__RefHeading__1774_1702457476)

[3.7 <span
lang="zh-CN">脚本出错处理</span>](#__RefHeading__1776_1702457476)[17](#__RefHeading__1776_1702457476)

[4<span
lang="zh-CN">部署</span>](#__RefHeading__1778_1702457476)[18](#__RefHeading__1778_1702457476)




<span lang="zh-CN">开发规范请参考《</span>lua<span
lang="zh-CN">脚本规范</span>.txt<span lang="zh-CN">》</span>

RPC<span lang="zh-CN">接口请参考《</span>RPCCommandV0.1 beta.docx<span
lang="zh-CN">》</span>

<span lang="zh-CN">原理请参考《</span>DACRS<span
lang="zh-CN">系统智能合约</span>LUA<span
lang="zh-CN">应用开发原理</span>.docx<span lang="zh-CN">》</span>

LUA SDK API<span lang="zh-CN">请参考《智能合约</span>API—LUA.docx<span
lang="zh-CN">》</span>



1.  

[]()[]() 1.1<span lang="zh-CN">由于安全性考虑，合约中只能使用</span>lua<span lang="zh-CN">中</span>table<span lang="zh-CN">，</span>math<span lang="zh-CN">，</span>string<span lang="zh-CN">库，不能使用</span>io<span lang="zh-CN">操作等。</span> {#由于安全性考虑合约中只能使用lua中tablemathstring库不能使用io操作等 .western style="margin-left: 0in; margin-top: 0.11in"}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[]()[]() 1.2<span lang="zh-CN">脚本现在只能写在一个文件中，不支持多文件。</span> {#脚本现在只能写在一个文件中不支持多文件 .western style="margin-left: 0in; margin-top: 0.11in"}
--------------------------------------------------------------------------------

[]()[]() 1.3<span lang="zh-CN">脚本大小不能超过</span>64k<span lang="zh-CN">。</span> {#脚本大小不能超过64k .western style="margin-left: 0in; margin-top: 0.11in"}
-------------------------------------------------------------------------------------

[]()[]() 1.4<span lang="zh-CN">合约内容通过全局变量“</span>contract”<span lang="zh-CN">传给脚本，脚本里面可以拿来就用</span> {#合约内容通过全局变量contract传给脚本脚本里面可以拿来就用 .western style="margin-left: 0in; margin-top: 0.11in"}
----------------------------------------------------------------------------------------------------------------------------

[]()[]() 1.5<span lang="zh-CN">账户平衡检测开关通过在</span>lua<span lang="zh-CN">脚本中的全局变量“</span>gCheckAccount”<span lang="zh-CN">控制，默认关闭此开关。</span> {#账户平衡检测开关通过在lua脚本中的全局变量gcheckaccount控制默认关闭此开关 .western style="margin-left: 0in; margin-top: 0.11in"}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[]()[]() 1.6<span lang="zh-CN">合约内容不能超过</span>4096<span lang="zh-CN">字节。</span> {#合约内容不能超过4096字节 .western align="left" style="margin-left: 0in; margin-top: 0.11in"}
------------------------------------------------------------------------------------------

[]()[]() 1.7<span lang="zh-CN">脚本中如果有异常，或逻辑不对，可以通过</span>assert<span lang="zh-CN">，</span>error<span lang="zh-CN">退出执行，</span>lua<span lang="zh-CN">解释器会捕获到该异常。</span> {#脚本中如果有异常或逻辑不对可以通过asserterror退出执行lua解释器会捕获到该异常 .western style="margin-left: 0in; margin-top: 0.11in"}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[]()[]() 1.8<span lang="zh-CN">脚本中必须以</span>mylib = require "mylib"<span lang="zh-CN">开头，通过</span>mylib<span lang="zh-CN">调用里面的</span>API<span lang="zh-CN">。</span> {#脚本中必须以mylib-require-mylib开头通过mylib调用里面的api .western style="margin-left: 0in; margin-top: 0.11in"}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

2.  

\
\
 {#section .western style="margin-top: 0.11in"}
-

<span lang="zh-CN">该示例所使用的</span>SDK API<span
lang="zh-CN">，请参考《智能合约</span>API—LUA.docx<span
lang="zh-CN">》，文档里有详细的例子。</span>

mylib = require "mylib"

\

\

\

--<span lang="zh-CN">日志类型</span>

LOG\_TYPE =

{

ENUM\_STRING = 0, --<span lang="zh-CN">字符串类型</span>

ENUM\_NUMBER = 1, --<span lang="zh-CN">数字类型 </span>

};

\

--<span lang="zh-CN">系统账户操作定义</span>

OPER\_TYPE =

{

ENUM\_ADD\_FREE = 1, --<span lang="zh-CN">系统账户加</span>

ENUM\_MINUS\_FREE = 2 --<span lang="zh-CN">系统账户减</span>

}

\

--<span lang="zh-CN">脚本应用账户操作类型定义</span>

APP\_OPERATOR\_TYPE =

{

ENUM\_ADD\_FREE\_OP = 1, --<span lang="zh-CN">自由账户加</span>

ENUM\_SUB\_FREE\_OP = 2, --<span lang="zh-CN">自由账户减</span>

ENUM\_ADD\_FREEZED\_OP = 3, --<span lang="zh-CN">冻结账户加</span>

ENUM\_SUB\_FREEZED\_OP = 4 --<span lang="zh-CN">冻结账户减</span>

}

\

--<span lang="zh-CN">账户类型</span>

ADDR\_TYPE =

{

ENUM\_REGID = 1, -- REG\_ID

ENUM\_BASE58 = 2, -- BASE58 ADDR

}

\

--<span lang="zh-CN">交易类型</span>

TX\_TYPE =

{

TX\_WITHDRAW = 1, --<span lang="zh-CN">提现</span>

TX\_RECHARGE= 2, --<span lang="zh-CN">充值</span>

}

\

FREEZE\_MONTH\_NUM = 20 -- <span lang="zh-CN">冻结次数</span>

FREEZE\_PERIOD = 5 -- <span lang="zh-CN">冻结周期</span>

\

MAX\_MONEY = 100000000000000000 -- <span lang="zh-CN">总金额限制</span>

FREE\_MONEY = 10000000000000000 -- <span
lang="zh-CN">自由金额限制</span>

\

gCheckAccount = true -- <span lang="zh-CN">平衡检查 </span>true <span
lang="zh-CN">打开，</span>false <span lang="zh-CN">关闭</span>

\

gSendAccountTbl = -- <span lang="zh-CN">发币地址</span>

{

0x00, 0x00, 0x00, 0x00, 0x01, 0x00

}

\

--<span lang="zh-CN">判断表是否为空</span>

function TableIsEmpty(t)

return \_G.next(t) == nil

end

\

--<span lang="zh-CN">判断表非空</span>

function TableIsNotEmpty(t)

return false == TableIsEmpty(t)

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span lang="zh-CN">日志输出</span>

<span lang="zh-CN">参数：</span>

aKey:<span lang="zh-CN">日志类型</span>

bLength:<span lang="zh-CN">日志长度</span>

cValue<span lang="zh-CN">：日志</span>

--\]\]

function LogPrint(aKey,bLength,cValue)

assert(bLength &gt;= 1,"LogPrint bLength invlaid")

if(aKey == LOG\_TYPE.ENUM\_STRING) then

assert(type(cValue) == "string","LogPrint cValue invlaid0")

elseif(aKey == LOG\_TYPE.ENUM\_NUMBER) then

assert(TableIsNotEmpty(cValue),"LogPrint cValue invlaid1")

else

error("LogPrint aKey invlaid")

end

\

local logTable = {

key = LOG\_TYPE.ENUM\_STRING,

length = 0,

value = nil

}

logTable.key = aKey

logTable.length = bLength

logTable.value = cValue

mylib.LogPrint(logTable)

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span lang="zh-CN">遍历表元素</span>

<span lang="zh-CN">参数：</span>

t:<span lang="zh-CN">表</span>

i:<span lang="zh-CN">开始索引</span>

--\]\]

function Unpack(t,i)

i = i or 1

if t\[i\] then

return t\[i\],Unpack(t,i+1)

end

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span
lang="zh-CN">比较两表元素是否相同</span>

<span lang="zh-CN">参数：</span>

tDest:<span lang="zh-CN">表</span>1

tSrc:<span lang="zh-CN">表</span>2

start1:<span lang="zh-CN">开始索引</span>

<span lang="zh-CN">返回值：</span>

0:<span lang="zh-CN">相等</span>

1:<span lang="zh-CN">表</span>1&gt;<span lang="zh-CN">表</span>2

2:<span lang="zh-CN">表</span>1&lt;<span lang="zh-CN">表</span>2

--\]\]

function MemCmp(tDest,tSrc,start1)

assert(TableIsNotEmpty(tDest),"tDest is empty")

assert(TableIsNotEmpty(tSrc),"tSrc is empty")

local i

for i = \#tDest,1,-1 do

if tDest\[i\] &gt; tSrc\[i + start1 - 1\] then

return 1

elseif tDest\[i\] &lt; tSrc\[i + start1 - 1\] then

return -1

else

end

end

return 0

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span
lang="zh-CN">获取表从开始索引指定长度的元素集合</span>

<span lang="zh-CN">参数：</span>

tbl:<span lang="zh-CN">表</span>

start:<span lang="zh-CN">开始索引</span>

length:<span lang="zh-CN">长度</span>

<span lang="zh-CN">返回值：</span>

<span lang="zh-CN">一个新表</span>

--\]\]

function GetValueFromContract(tbl,start,length)

assert(start &gt; 0,"GetValueFromContract start err")

assert(length &gt; 0,"GetValueFromContract length err")

local newTab = {}

local i

for i = 0,length -1 do

newTab\[1 + i\] = tbl\[start + i\]

end

return newTab

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span lang="zh-CN">充值</span>

<span lang="zh-CN">参数：</span>

<span lang="zh-CN">无</span>

<span lang="zh-CN">返回值：</span>

true:<span lang="zh-CN">成功</span>

false:<span lang="zh-CN">失败</span>

<span lang="zh-CN">流程：</span>

1<span lang="zh-CN">）获取当前交易账户，并判断是否与发币地址一致</span>

2<span lang="zh-CN">）获取合约相应内容，并判断合法性</span>

3<span lang="zh-CN">）将自由金额提现到系统账户下</span>

4<span lang="zh-CN">）冻结相应的冻结部分</span>

5<span lang="zh-CN">）扣除相应的脚本账户下的金额</span>

--\]\]

function Recharge()

-- 1<span lang="zh-CN">）</span>

-- local accountTbl = {0, 0, 0, 0, 0, 0}

-- accountTbl = {mylib.GetCurTxAccount()}

-- assert(TableIsNotEmpty(accountTbl),"GetCurTxAccount error")

-- assert(MemCmp(gSendAccountTbl, accountTbl,1) == 0,"Recharge address
err")

-- 2<span lang="zh-CN">）</span>

local toAddrTbl = {}

toAddrTbl = GetValueFromContract(contract, 3, 34)

local moneyTbl = {}

moneyTbl = GetValueFromContract(contract, 37, 8)

local money = mylib.ByteToInteger(Unpack(moneyTbl))

assert(money &gt; 0,"money &lt;= 0")

local freeMoneyTbl = {}

freeMoneyTbl = GetValueFromContract(contract, 45, 8)

local freeMoney = mylib.ByteToInteger(Unpack(freeMoneyTbl))

assert(freeMoney &gt; 0,"freeMoney &lt;= 0")

local freeMonthMoneyTbl = {}

freeMonthMoneyTbl = GetValueFromContract(contract, 53, 8)

local freeMonthMoney = mylib.ByteToInteger(Unpack(freeMonthMoneyTbl))

assert(freeMonthMoney &gt; 0,"freeMonthMoney &lt;= 0")

local payMoneyTbl = {}

payMoneyTbl = {mylib.GetCurTxPayAmount()}

assert(TableIsNotEmpty(payMoneyTbl),"GetCurTxPayAmount error")

local payMoney = mylib.ByteToInteger(Unpack(payMoneyTbl))

assert(payMoney &gt; 0,"payMoney &lt;= 0")

-- <span lang="zh-CN">总金额与充值金额要相等</span>

assert(money == payMoney, "<span lang="zh-CN">充值金额不正确</span>1")

-- <span lang="zh-CN">总金额不能小于</span>1,<span
lang="zh-CN">不能小于自由金额或月冻结金额</span>

if money &lt; 1

or money &lt; freeMoney

or money &lt; freeMonthMoney then

LogPrint(LOG\_TYPE.ENUM\_STRING, string.len("<span
lang="zh-CN">充值金额不正确</span>2"), "<span
lang="zh-CN">充值金额不正确</span>2");

error("<span lang="zh-CN">充值金额不正确</span>2")

end

-- <span lang="zh-CN">三个金额，上限值检测</span>

if money &gt;= MAX\_MONEY

or freeMoney &gt;= FREE\_MONEY

or freeMonthMoney &gt;= FREE\_MONEY then

LogPrint(LOG\_TYPE.ENUM\_STRING, string.len("<span
lang="zh-CN">充值金额不正确</span>3"), "<span
lang="zh-CN">充值金额不正确</span>3");

error("<span lang="zh-CN">充值金额不正确</span>3")

end

local freezeNum = FREEZE\_MONTH\_NUM - 1

assert(freezeNum &gt; 0, "<span lang="zh-CN">月冻结总数不正确</span>")

-- <span lang="zh-CN">总金额不能小于总的月冻结金额</span>

local freezeMoney = freeMonthMoney \* freezeNum

if freezeMoney &lt; freezeNum

or freezeMoney &lt; freeMoney

or money &lt; freezeMoney then

LogPrint(LOG\_TYPE.ENUM\_STRING, string.len("<span
lang="zh-CN">充值金额不正确</span>4"), "<span
lang="zh-CN">充值金额不正确</span>4");

error("<span lang="zh-CN">充值金额不正确</span>4")

end

-- <span
lang="zh-CN">检查充值总金额和自由金额加上冻结金额是否相等</span>

freezeMoney = freezeMoney + freeMoney

if money \~= freezeMoney then

LogPrint(LOG\_TYPE.ENUM\_STRING, string.len("<span
lang="zh-CN">充值金额不正确</span>5"), "<span
lang="zh-CN">充值金额不正确</span>5");

error("<span lang="zh-CN">充值金额不正确</span>5")

end

-- 3<span lang="zh-CN">）</span>

--<span lang="zh-CN">操作系统账户的结构</span>

local writeOutputTbl =

{

addrType = 1, --<span lang="zh-CN">账户类型 </span>REG\_ID =
0x01,BASE\_58\_ADDR = 0x02,

accountIdTbl = {}, --account id

operatorType = 0, --<span lang="zh-CN">操作类型</span>

outHeight = 0, --<span lang="zh-CN">超时高度</span>

moneyTbl = {} --<span lang="zh-CN">金额</span>

}

\

writeOutputTbl.addrType = ADDR\_TYPE.ENUM\_BASE58

writeOutputTbl.operatorType = OPER\_TYPE.ENUM\_ADD\_FREE

writeOutputTbl.accountIdTbl = {Unpack(toAddrTbl)}

writeOutputTbl.moneyTbl = {Unpack(freeMoneyTbl)}

assert(mylib.WriteOutput(writeOutputTbl),"WriteOutput err1")

local curHeight = 0

curHeight = mylib.GetCurRunEnvHeight()

-- 4<span lang="zh-CN">）</span>

local appOperateTbl = {

operatorType = 0, -- <span lang="zh-CN">操作类型</span>

outHeight = 0, -- <span lang="zh-CN">超时高度</span>

moneyTbl = {},

userIdLen = 0, -- <span lang="zh-CN">地址长度</span>

userIdTbl = {}, -- <span lang="zh-CN">地址</span>

fundTagLen = 0, -- fund tag len

fundTagTbl = {} -- fund tag

}

appOperateTbl.operatorType = APP\_OPERATOR\_TYPE.ENUM\_ADD\_FREEZED\_OP

appOperateTbl.userIdLen = 34

appOperateTbl.userIdTbl = toAddrTbl

appOperateTbl.moneyTbl = freeMonthMoneyTbl

for i = 1, freezeNum do

appOperateTbl.outHeight = curHeight + FREEZE\_PERIOD \* i

assert(mylib.WriteOutAppOperate(appOperateTbl),"WriteOutAppOperate
err1")

end

-- 5<span lang="zh-CN">）</span>

writeOutputTbl.addrType = ADDR\_TYPE.ENUM\_REGID

writeOutputTbl.operatorType = OPER\_TYPE.ENUM\_MINUS\_FREE

writeOutputTbl.accountIdTbl = {mylib.GetScriptID()}

assert(mylib.WriteOutput(writeOutputTbl),"WriteOutput err2")

return true

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span lang="zh-CN">操作系统账户</span>

<span lang="zh-CN">参数：</span>

accTbl:<span lang="zh-CN">账户</span>

moneyTbl:<span lang="zh-CN">操作金额</span>

<span lang="zh-CN">返回值：</span>

true:<span lang="zh-CN">成功</span>

false:<span lang="zh-CN">失败</span>

<span lang="zh-CN">流程：</span>

1<span lang="zh-CN">）增加该系统账户金额</span>

2<span lang="zh-CN">）相应地减少脚本账户金额</span>

--\]\]

function WriteWithdrawal(accTbl,moneyTbl)

--<span lang="zh-CN">操作系统账户的结构</span>

local writeOutputTbl =

{

addrType = 1, --<span lang="zh-CN">账户类型 </span>REG\_ID =
0x01,BASE\_58\_ADDR = 0x02,

accountIdTbl = {}, --account id

operatorType = 0, --<span lang="zh-CN">操作类型</span>

outHeight = 0, --<span lang="zh-CN">超时高度</span>

moneyTbl = {} --<span lang="zh-CN">金额</span>

}

--<span lang="zh-CN">执行系统账户提现操作</span>

assert(TableIsNotEmpty(accTbl),"WriteWithDrawal accTbl invlaid1")

assert(TableIsNotEmpty(moneyTbl),"WriteWithDrawal moneyTbl invlaid1")

-- 1<span lang="zh-CN">）</span>

writeOutputTbl.addrType = ADDR\_TYPE.ENUM\_REGID

writeOutputTbl.operatorType = OPER\_TYPE.ENUM\_ADD\_FREE

writeOutputTbl.accountIdTbl = {Unpack(accTbl)}

writeOutputTbl.moneyTbl = {Unpack(moneyTbl)}

assert(mylib.WriteOutput(writeOutputTbl),"WriteWithDrawal WriteOutput
err0")

-- 2<span lang="zh-CN">）</span>

writeOutputTbl.operatorType = OPER\_TYPE.ENUM\_MINUS\_FREE

writeOutputTbl.accountIdTbl = {mylib.GetScriptID()}

assert(mylib.WriteOutput(writeOutputTbl),"WriteWithDrawal WriteOutput
err1")

return true

end

\

--\[\[

<span lang="zh-CN">功能</span>:<span lang="zh-CN">提现</span>

<span lang="zh-CN">参数：</span>

addrType:<span lang="zh-CN">账户类型，</span>BASE58<span
lang="zh-CN">或</span>REGID

<span lang="zh-CN">返回值：</span>

true:<span lang="zh-CN">成功</span>

false:<span lang="zh-CN">失败</span>

<span lang="zh-CN">流程：</span>

1<span lang="zh-CN">）判断账户类型</span>

2<span lang="zh-CN">）获取当前交易账户</span>

3<span lang="zh-CN">）获取该账户下的自由金额</span>

4<span lang="zh-CN">）减掉该账户下的自由金额</span>

5<span lang="zh-CN">）相应的操作系统账户</span>

--\]\]

function Withdraw(addrType)

-- 1<span lang="zh-CN">）</span>

if addrType \~= ADDR\_TYPE.ENUM\_REGID and addrType \~=
ADDR\_TYPE.ENUM\_BASE58 then

error("In function Withdraw, addr type err")

end

-- 2<span lang="zh-CN">）</span>

local accountTbl = {0, 0, 0, 0, 0, 0}

accountTbl = {mylib.GetCurTxAccount()}

assert(TableIsNotEmpty(accountTbl),"GetCurTxAccount error")

local idTbl =

{

idLen = 0,

idValueTbl = {}

}

if addrType == ADDR\_TYPE.ENUM\_REGID then

idTbl.idLen = 6

idTbl.idValueTbl = accountTbl

else

local base58Addr = {}

base58Addr = {mylib.GetBase58Addr(Unpack(accountTbl))}

assert(TableIsNotEmpty(base58Addr),"GetBase58Addr error")

idTbl.idLen = 34

idTbl.idValueTbl = base58Addr

end

-- 3<span lang="zh-CN">）</span>

local freeMoneyTbl = {mylib.GetUserAppAccValue(idTbl)}

assert(TableIsNotEmpty(freeMoneyTbl),"GetUserAppAccValue error")

local freeMoney = mylib.ByteToInteger(Unpack(freeMoneyTbl))

assert(freeMoney &gt; 0,"Account balance is 0.")

-- 4<span lang="zh-CN">）</span>

local appOperateTbl = {

operatorType = 0, -- <span lang="zh-CN">操作类型</span>

outHeight = 0, -- <span lang="zh-CN">超时高度</span>

moneyTbl = {},

userIdLen = 0, -- <span lang="zh-CN">地址长度</span>

userIdTbl = {}, -- <span lang="zh-CN">地址</span>

fundTagLen = 0, -- fund tag len

fundTagTbl = {} -- fund tag

}

appOperateTbl.operatorType = APP\_OPERATOR\_TYPE.ENUM\_SUB\_FREE\_OP

appOperateTbl.userIdLen = idTbl.idLen

appOperateTbl.userIdTbl = idTbl.idValueTbl

appOperateTbl.moneyTbl = freeMoneyTbl

assert(mylib.WriteOutAppOperate(appOperateTbl),"WriteOutAppOperate
err1")

-- 5<span lang="zh-CN">）</span>

assert(WriteWithdrawal(accountTbl, freeMoneyTbl), "WriteWithdrawal err")

return true

end

\

\

function Main()

--\[\[

local i = 1

for i = 1,\#contract do

print("contract")

print(" ",i,(contract\[i\]))

end

--\]\]

assert(\#contract &gt;= 2,"contract length err.")

assert(contract\[1\] == 0xff,"Contract identification error.")

\

if contract\[2\] == TX\_TYPE.TX\_RECHARGE then

assert(\#contract == 60,"recharge contract length err.")

Recharge()

elseif contract\[2\] == TX\_TYPE.TX\_WITHDRAW then

assert(\#contract == 11,"withdraw contract length err.")

Withdraw(contract\[3\])

else

error("RUN\_SCRIPT\_DATA\_ERR")

end

\

end

\

Main()

\

3.  

<span
lang="zh-CN">以上面的示例代码为例，将其代码保存为</span>test.lua<span
lang="zh-CN">，文件格式保存为</span>utf-8<span lang="zh-CN">：</span>

[]()[]() 3.1 <span lang="zh-CN">启动</span>dacrs<span lang="zh-CN">程序</span> {#启动dacrs程序 .western style="margin-left: 0in; margin-top: 0.11in"}
------------------------------------------------------------------------------

<span lang="zh-CN">最好在</span>linux<span
lang="zh-CN">下测试，</span>windows<span
lang="zh-CN">上编译，调试慢。调试时先在</span>regtest<span
lang="zh-CN">下调试通过，然后才在</span>testnet<span
lang="zh-CN">和</span>main<span lang="zh-CN">网络上注册。</span>

<span lang="zh-CN">修改</span>Dacrs.conf<span
lang="zh-CN">文件，添加</span>regtest=1<span
lang="zh-CN">，打开</span>vm<span
lang="zh-CN">调试开关，</span>debug=vm<span
lang="zh-CN">，注释掉</span>gen=1<span
lang="zh-CN">，</span>genproclimit=1000000<span
lang="zh-CN">，采用手动挖矿。</span>

![](data:image/png;base64,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){width="244"
height="311"}

\

<span lang="zh-CN">下面所用到的</span>RPC<span
lang="zh-CN">命令，请参考</span>RPC<span
lang="zh-CN">接口文档《</span>RPCCommandV0.1 beta.docx<span
lang="zh-CN">》。</span>

\

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test

Dacrs version v1.1.2.5-8a88c65-dirty-release-linux (2016-10-11 10:03:03
+0800)

Using OpenSSL version OpenSSL 1.0.1f 6 Jan 2014

Startup time: 2016-10-11 08:14:26

Default data directory /home/xgc/.Dacrs

Using data directory /home/share/xgc/dacrs\_test/regtest

Using at most 125 connections ( 1024 file descriptors available)

\

[]()[]() 3.2 <span lang="zh-CN">导入私钥</span> {#导入私钥 .western style="margin-left: 0in; margin-top: 0.11in"}
-----------------------------------------------

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test importprivkey
cNcJkU44oG3etbWoEvY46i5qWPeE8jVb7K44keXxEQxsXUZ85MKU

{

"imorpt key address" : "dk2NNjraSvquD9b4SQbysVRQeFikA55HLi"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getaccountinfo
dk2NNjraSvquD9b4SQbysVRQeFikA55HLi

{

"Address" : "dk2NNjraSvquD9b4SQbysVRQeFikA55HLi",

"KeyID" : "4fb64dd1d825bb6812a7090a1d0dd2c75b55242e",

"RegID" : "0-20",

"PublicKey" :
"03ae28a4100145a4c354338c727a54800dc540069fa2f5fd5d4a1c80b4a35a1762",

"MinerPKey" : "",

"Balance" : 100000082000000000,

"CoinDays" : 0,

"UpdateHeight" : 263,

"CurCoinDays" : 694445,

"postion" : "inblock"

}

\

[]()[]() 3.3 <span lang="zh-CN">生成几个测试地址，并充值激活</span> {#生成几个测试地址并充值激活 .western style="margin-left: 0in; margin-top: 0.11in"}
-------------------------------------------------------------------

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getnewaddress

{

"addr" : "druMpuM8YEkvzyErLMUgwasyafoficmK7S",

"minerpubkey" : "no"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getnewaddress

{

"addr" : "dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6",

"minerpubkey" : "no"

}

<span lang="zh-CN">充币：</span>

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test sendtoaddress
druMpuM8YEkvzyErLMUgwasyafoficmK7S 100000000000

{

"hash" :
"59b55b1abe2a6aa38d85301158d486ffa367f349af9c18506a4adadc1d999a41"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test sendtoaddress
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6 100000000000

{

"hash" :
"e6ac958bbc202cb300bbfcb21ed66e6279f009128ec17e9354796e3d12ae5dd5"

}

<span lang="zh-CN">手动挖矿，看生成的两地址里现在是否有币</span>

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test setgenerate true 1

{

"msg" : "in mining"

}

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getbalance
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

{

"balance" : 1000.00000000

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getbalance
druMpuM8YEkvzyErLMUgwasyafoficmK7S

{

"balance" : 1000.00000000

}

<span lang="zh-CN">激活这两个地址</span>

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test registaccounttx
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6 100000

{

"hash" :
"02d86cdecb3cb9a9d92bd28cd6023c58f771bd3df03aa0689e91b26c2307a976"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test registaccounttx
druMpuM8YEkvzyErLMUgwasyafoficmK7S 100000

{

"hash" :
"6638af4edc5e417d8abd214bb6c1db1f41f83ea2e4b8c5924d2bcebfe4e25741"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test setgenerate true 1

{

"msg" : "in mining"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getaccountinfo
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

{

"Address" : "dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6",

"KeyID" : "8dfa4bec33ea7ce2692a6dc4ea3e47e1085cc0b7",

"RegID" : "293-1",

"PublicKey" :
"0208f52f6e296805bb8aa44a3c44454cc15ed5abca43b9f95ae73f1ef2c99f2bc1",

"MinerPKey" : "",

"Balance" : 99999900000,

"CoinDays" : 9,

"UpdateHeight" : 293,

"CurCoinDays" : 9,

"postion" : "inblock"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getaccountinfo
druMpuM8YEkvzyErLMUgwasyafoficmK7S

{

"Address" : "druMpuM8YEkvzyErLMUgwasyafoficmK7S",

"KeyID" : "9b2bd08576843e5416c7a90739b8ea50d4e98b4f",

"RegID" : "293-2",

"PublicKey" :
"027826fbe5ce964c4bd1d55217d103f21214ef603da24224b9d4eee182a2353d32",

"MinerPKey" : "",

"Balance" : 99999900000,

"CoinDays" : 9,

"UpdateHeight" : 293,

"CurCoinDays" : 9,

"postion" : "inblock"

}

RegID<span lang="zh-CN">字段分别为</span>293-1,293-2,<span
lang="zh-CN">表示地址已经激活。</span>

\

[]()[]() 3.4 <span lang="zh-CN">注册应用脚本</span> {#注册应用脚本 .western style="margin-left: 0in; margin-top: 0.11in"}
---------------------------------------------------

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test registerapptx
druMpuM8YEkvzyErLMUgwasyafoficmK7S
/home/share/xgc/dacrs\_test/data/test.lua 110000000 0 "test"

{

"hash" :
"b9e8906135e64eec879a0dc38079031346dccb0ba273b5503dcd7f3bb0e42e6f"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test setgenerate true 1

{

"msg" : "in mining"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getscriptid
b9e8906135e64eec879a0dc38079031346dccb0ba273b5503dcd7f3bb0e42e6f

{

"regid:" : "295-1",

"script" : "270100000100"

}

<span lang="zh-CN">获取到脚本</span>appid<span
lang="zh-CN">为</span>295-1

\

[]()[]() 3.5 <span lang="zh-CN">充值操作</span> {#充值操作 .western style="margin-left: 0in; margin-top: 0.11in"}
-----------------------------------------------

\

<span lang="zh-CN">合约内容</span>=<span lang="zh-CN">前缀</span>1<span
lang="zh-CN">字节（</span>0xff<span lang="zh-CN">）</span>+ <span
lang="zh-CN">操作类型</span>1<span lang="zh-CN">字节（</span>0x02<span
lang="zh-CN">）</span>+ <span lang="zh-CN">充值地址</span>34<span
lang="zh-CN">字节（</span>dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6<span
lang="zh-CN">）</span>+ <span lang="zh-CN">充值总金额 </span>8<span
lang="zh-CN">字节（</span>10000000000<span lang="zh-CN">）</span>+ <span
lang="zh-CN">自由金额 </span>8<span
lang="zh-CN">字节（</span>500000000<span lang="zh-CN">）</span>+ <span
lang="zh-CN">每月冻结金额 </span>8<span
lang="zh-CN">字节（</span>500000000<span lang="zh-CN">）</span>

\

<span lang="zh-CN">将合约内容转换成</span>16<span
lang="zh-CN">进制字符串</span>

<span lang="zh-CN">前缀（</span>0xff<span lang="zh-CN">）</span>=&gt; ff

<span lang="zh-CN">操作类型（</span>0x02<span
lang="zh-CN">）</span>=&gt; 02

\

<span
lang="zh-CN">充值地址（</span>dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6<span
lang="zh-CN">）</span>=&gt;

d<span lang="zh-CN">的</span>ascii<span lang="zh-CN">码</span>10<span
lang="zh-CN">进制是</span>100<span lang="zh-CN">，转成</span>16<span
lang="zh-CN">进制是</span>64

q<span lang="zh-CN">的</span>ascii<span lang="zh-CN">码</span>10<span
lang="zh-CN">进制是</span>113<span lang="zh-CN">，转成</span>16<span
lang="zh-CN">进制是</span>71

<span
lang="zh-CN">依次转换，最终结果为</span>6471686269716a705436376f555832615458753366416362707670634a4556345936

\

<span lang="zh-CN">充值总金额（</span>10000000000<span
lang="zh-CN">）</span>=&gt;

<span lang="zh-CN">利用计算器转成</span>16<span
lang="zh-CN">进制为</span>2540be400<span
lang="zh-CN">，补齐</span>8<span lang="zh-CN">字节后为</span>00 00 00 02
54 0b e4 00<span
lang="zh-CN">，按照内存中逆序后为</span>00e40b5402000000

\

<span lang="zh-CN">自由金额（</span>500000000<span
lang="zh-CN">）</span>=&gt;

<span lang="zh-CN">利用计算器转成</span>16<span
lang="zh-CN">进制为</span>1dcd6500<span lang="zh-CN">，补齐</span>8<span
lang="zh-CN">字节后为</span>00 00 00 00 1d cd 65 00<span
lang="zh-CN">，按照内存中逆序后为</span>0065cd1d00000000

\

<span lang="zh-CN">每月冻结金额（</span>500000000<span
lang="zh-CN">）</span>=&gt;

<span lang="zh-CN">利用计算器转成</span>16<span
lang="zh-CN">进制为</span>1dcd6500<span lang="zh-CN">，补齐</span>8<span
lang="zh-CN">字节后为</span>00 00 00 00 1d cd 65 00<span
lang="zh-CN">，按照内存中逆序后为</span>0065cd1d00000000

\

<span lang="zh-CN">将这些字段组合在一起，形成合约内容：</span>

ff026471686269716a705436376f555832615458753366416362707670634a455634593600e40b54020000000065cd1d000000000065cd1d00000000

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test createcontracttx
druMpuM8YEkvzyErLMUgwasyafoficmK7S 295-1 10000000000
ff026471686269716a705436376f555832615458753366416362707670634a455634593600e40b54020000000065cd1d000000000065cd1d00000000
100000 0

{

"hash" :
"fadb05dca69b2a9a5ee771ec6533b2b856950868af8589476e920c2eea5a465c"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test setgenerate true 1

{

"msg" : "in mining"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getappaccinfo 295-1
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

{

"mAccUserID" :
"6471686269716a705436376f555832615458753366416362707670634a4556345936",

"FreeValues" : 0,

"vFreezedFund" : \[

{

"value" : 500000000,

"nHeight" : 309,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 314,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 319,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 324,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 329,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 334,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 339,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 344,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 349,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 354,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 359,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 364,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 369,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 374,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 379,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 384,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 389,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 394,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 399,

"vTag" : ""

}

\]

}

\

<span lang="zh-CN">手动多挖几次矿，等自由金额不为</span>0<span
lang="zh-CN">时，可以提现操作</span>

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getappaccinfo 295-1
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

{

"mAccUserID" :
"6471686269716a705436376f555832615458753366416362707670634a4556345936",

"FreeValues" : 500000000,

"vFreezedFund" : \[

{

"value" : 500000000,

"nHeight" : 314,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 319,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 324,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 329,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 334,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 339,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 344,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 349,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 354,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 359,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 364,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 369,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 374,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 379,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 384,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 389,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 394,

"vTag" : ""

},

{

"value" : 500000000,

"nHeight" : 399,

"vTag" : ""

}

\]

}

[]()[]() 3.6 <span lang="zh-CN">提现操作</span> {#提现操作 .western style="margin-left: 0in; margin-top: 0.11in"}
-----------------------------------------------

<span lang="zh-CN">将自由金额（</span>5<span
lang="zh-CN">个币），提现到地址</span>dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

\

<span lang="zh-CN">合约内容</span>=<span lang="zh-CN">前缀</span>1<span
lang="zh-CN">字节（</span>0xff<span lang="zh-CN">）</span>+ <span
lang="zh-CN">操作类型</span>1<span lang="zh-CN">字节（</span>0x01<span
lang="zh-CN">）</span>+ <span lang="zh-CN">账户类型</span>1<span
lang="zh-CN">字节（</span>0x02<span lang="zh-CN">）</span>+ <span
lang="zh-CN">提现金额 </span>8<span
lang="zh-CN">字节（</span>500000000<span lang="zh-CN">）</span>

\

<span lang="zh-CN">将合约内容转换成</span>16<span
lang="zh-CN">进制字符串</span>

<span lang="zh-CN">前缀（</span>0xff<span lang="zh-CN">）</span>=&gt; ff

<span lang="zh-CN">操作类型（</span>0x02<span
lang="zh-CN">）</span>=&gt; 01

<span lang="zh-CN">账户类型（</span>0x02<span
lang="zh-CN">）</span>=&gt; 02

<span lang="zh-CN">提现金额（</span>500000000<span
lang="zh-CN">）</span>=&gt;

<span lang="zh-CN">利用计算器转成</span>16<span
lang="zh-CN">进制为</span>1dcd6500<span lang="zh-CN">，补齐</span>8<span
lang="zh-CN">字节后为</span>00 00 00 00 1d cd 65 00<span
lang="zh-CN">，按照内存中逆序后为</span>0065cd1d00000000

\

<span lang="zh-CN">将这些字段组合在一起，形成合约内容：</span>

ff01020065cd1d00000000

\

### []()[]() 3.6.1<span lang="zh-CN">查看</span>dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6<span lang="zh-CN">当前余额 ：</span> {#查看dqhbiqjpt67oux2atxu3facbpvpcjev4y6当前余额 .western style="margin-left: 0in; margin-top: 0.11in"}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getbalance
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

{

"balance" : 1004.99900000

}

\

### []()[]() 3.6.2<span lang="zh-CN">提现</span> {#提现 .western style="margin-left: 0in; margin-top: 0.11in"}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test createcontracttx
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6 295-1 0 ff01020065cd1d00000000 100000
0

{

"hash" :
"ce0cf0817e91780b1f7fa1b63ce0af6cbd788024f0c3c15080c2b6748f12e144"

}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test setgenerate true 1

{

"msg" : "in mining"

}

\

### []()[]() 3.6.3 <span lang="zh-CN">再次查看</span>dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6<span lang="zh-CN">当前余额 ，发现已经提现了</span>5<span lang="zh-CN">个币。</span> {#再次查看dqhbiqjpt67oux2atxu3facbpvpcjev4y6当前余额-发现已经提现了5个币 .western style="margin-left: 0in; margin-top: 0.11in"}

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test getbalance
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6

{

"balance" : 1009.99800000

}

[]()[]() 3.7 <span lang="zh-CN">脚本出错处理</span> {#脚本出错处理 .western style="margin-left: 0in; margin-top: 0.11in"}
---------------------------------------------------

<span
lang="zh-CN">假如现在再次提现一次，因为</span>dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6<span
lang="zh-CN">脚本账号下自由金额为</span>0<span
lang="zh-CN">，故提现操作会失败，要查看出错信息，修改</span>Dacrs.conf<span
lang="zh-CN">文件，打开</span>vm<span
lang="zh-CN">调试开关，</span>debug=vm<span lang="zh-CN">。</span>

<span lang="zh-CN">排错主要靠</span>LogPrint<span
lang="zh-CN">，</span>assert<span lang="zh-CN">，</span>error<span
lang="zh-CN">打印出错信息到日志。</span>

\

xgc@rangershi-MS-7817:/home/share/xgc/dacrs/src\$ ./dacrs-d
-datadir=/home/share/xgc/dacrs\_test createcontracttx
dqhbiqjpT67oUX2aTXu3fAcbpvpcJEV4Y6 295-1 0 ff01020065cd1d00000000 100000
0

error: {"code":-4,"message":"Error:run-script-error"}

<span lang="zh-CN">打开</span>regtest<span
lang="zh-CN">目录下的</span>vm.log:

\

2016-10-12 02:12:49 \[txmempool.cpp:125\]vm: tx
hash=69a787e4c7a35f40eff5f696c9f361972a9cb8a7e1e4263e527e689b9bd23e2c
CheckTxInMemPool run contract

2016-10-12 02:12:49 \[vm/vmrunevn.cpp:125\]vm: tx
hash:69a787e4c7a35f40eff5f696c9f361972a9cb8a7e1e4263e527e689b9bd23e2c
fees=100000 fuelrate=100 maxstep:90000

2016-10-12 02:12:49 \[vm/vmrunevn.cpp:93\]vm: CVmScriptRun::intial() LUA

2016-10-12 02:12:49 \[vm/vmlua.cpp:252\]vm: pVmScriptRun=0x7fa006ffb480

2016-10-12 02:12:49 \[vm/vmlua.cpp:259\]vm: luaL\_loadbuffer
fail:\[string "line"\]:375: Account balance is 0.

2016-10-12 02:12:49 \[vm/vmlua.cpp:262\]vm: run step=-1

2016-10-12 02:12:49 \[vm/vmrunevn.cpp:136\]vm: CVmScriptRun::run() LUA

\

<span lang="zh-CN">其中</span>luaL\_loadbuffer fail:\[string
"line"\]:375: Account balance is 0.<span
lang="zh-CN">提示了脚本</span>375<span
lang="zh-CN">行账户余额为</span>0<span
lang="zh-CN">，从而知道合约为啥会执行不成功。</span>

<span
lang="zh-CN">如果在开发过程中，边写代码边调试，可能写的代码有语法错误，在执行时也会出错，通过上面的方法可以查看出错误行。将错误修正后，要重新注册该脚本，再进行调试。</span>

\

4.  

<span
lang="zh-CN">在局域网测试完毕后，可以先在测试网络再测试一遍，然后部署到主网络。</span>

<span lang="zh-CN">修改配置文件</span>Dacrs.conf<span
lang="zh-CN">。</span>

<span lang="zh-CN">测试网络配置文件修改：</span>

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAANUAAAE4CAIAAABDjyE8AAAkhUlEQVR4nO2dz2si2drHj3D/AO3N23A3dq4KIy56hiwGXaVpBkyGITSDi4GmN0EX94IykJ3MonEXGBTuLJRsmoZehCaEoRPh0nRWhlk0PVmEDEQ74+IucjeT/Ae+50eVlp7nGE9V6SnL5wMzXTmeX6WPT52q8/V5/vbf//6XLJy///3vix8UCSB/Mz0BZKVxYX/90/33n8k/nu5sxH2fDjI7vUYueVkdNPOmJ+IFbfvrn74nT3fWP53OYzYrBLWevVTHi/Ekyp2Bf/MxhLb9xTd24oScf/Jh7EYuUjnL1uuZSqVF/yyeDNK1SIXUTzKVTVZAsvVup5xgR+y7XjnjZcUiIdud7aPIZou2aObFS9n6oFMer1nMZklVfMLtUkT06OhSHp33OT5FPoLUJ6+YzWbPzlgHpEJfs/odDSRawgM1iVUtct9psi5GfY46tctGo/CmhM9pvM9gY3L9R7+/Kfo+VjIng4HlB/Inl5HNTbuAfnKlFH2D26XkQaE76CSstzmzTfLNQf2ixJokeDe5K9FBe8+u2aZlu6wX2mSTWD3S4xeNMrdUaPQBNQ0Zqc9Evlu/4FOq7kVq6e7g1XFur0unQk3GMghas9HLcwsABiLNQTct+T/gNMcmz6wu1+B2RU+fTrWRKw0b07eBvXe0bod/YV4ck3LZl49prhi//6Bf1PGLEPVkdkG5Wsxd9Ujy6qJYbYovM7O2aW9rfjuzmaROVPS0y/7pXp6R1mZk6NmyjV7Zdg1jozscjQ33L0Cf7KUq83ckW9gauZneVW1zc5NM1ARPU6YHnWb7ktR37Yb53XrNsnOYrFU3kcqQq+mjBQTj9idxVim1y+KzatRamWqTvZutoza1g8mqF9Q48wn6ba+1SMHyXMIzcKh7YD0l09lsvdO53xk4mipfsPoE2/caLw4Kg0GHHbeHHlnNBa0hLu7U7VGvBp1mMk2ORhbXvSTprXvPY5nQtr/zw/2Pf/Gj/c/Ey13wcK3T4q5luJKhK6zNSIRXYYsYVpZvnhxFrDIyrLtVIEnhlrLZ4lmFX6qJ04Wx5oT5kleFXMTyX3Zr1egAbalPeqFkbSPk5IR+XZKlVDdNPWwu3a1mko6BWmxGScVAiXKBRCJ2GffH4GmWq8RRRosSzmWiWEKySW0d5zZbZ2LMq9Fh0G+Ote3v8bOdx76MrLySFpqDzqQbglzTRAfiZdCFAUPddx2fOnbCUWId5a3e5OGVAwEvQKcJlIGTd5TlZz434wTr+tsQX9xIZVlu3xCPBMv+ZndKSDgIlv0hqwbaH2IStD/EJGh/iEn07U/IXygP1neePfZ7PiGBPzOc9lDRh+YrqX8R8hcmQaB2eHgef/Y4OodZLT2j7en5NV9J/YuQv/CjR09JPOplbC/6F2VNSIECi2Kkwis2H6sr60Uhq4EUKICqZUwoc1In49MZIqpC85Sa80qQ0Gbl9S/sKkwdYdzL2F70L0LtIdUkoAIFEMVAhflX9YO9lPjYuJyEFpdVChRg8nyaYv+X2cdZ8WTKnrI8T6B5vqkQ2qy0/uXu/PDtx5hP+mcP+he5Zj4BKlBAAQtQmEhlLq5I25IWpkmBmeI0BcrY5IV+xapnX0BV/k+eJ9ic1weENso3M/T6F6Y/IOs7Pm0CA8yuf5FrqhQooIAFKKQ2eVQ6uqh3Ty5f5A4yVWbpMytQ2DRrjWZe6KZK9Fqp9H/QPMHmoUfT/u7Or5n45eM+NUJ2B/y9+/sPz/oXqGa5molMKlDysoCFQKoWRjJ90aKWkcj3CrW9lCVUmaZAcU6eXi2vhkIbuqZkkpgBqPtKgPOUm18U+XJuUmhDiqTVWkn9S9Q3+Yt3/QtYc0YFiarH4aToQXNKVcXkx4vhdd+U4cHmsNCmKTVG/Yt3Zte/oFImHATL/mbXv6BSJhwEy/6QVQPtDzEJ2h9iErQ/xCRu7M/+CZynEDBs/5TU5cdj8s6mDpq6E48SEv8VKOLsJ0+A7zWTifdk9sIg42b/43rt+51nUbYFfNp3bYFif1Uul3c2deAbpnszV/coIfFbgdIusf3bem3s3KmRWxvV1DhL7YGtnZixMOCY+/0lZ7gLcc9jPEiBAkdLGatPe61eJj1LSCD5DOinx3d7i0OFwUT0GWWghSaTMjRqY68cH2SqHT6N/Haxxn+yrlMYcFzrD/7i19+4p8HPKpCARQJWoEDRUpwMDcOzhASUzyj8tGVhjVyOvLKdkhR9Ri2Kufcdu2zLZjV7YfBwY3/WJhwXoHqSQEMCFqBaF1KgEHVQGBbshVqf4833JiGB479A5Jsdoey7oGaYsCYvR59J7SlEgfeSTQOVZi8MHtr6g8O3t1+JRV809uCv2z4hcdeDywIWEFCBogwKY4dSyzXgvX8XzBj/hYzuf6gZ0posvhUYfUbH/20VyLH4YvauLjIp3cKAo68/eHq6v7/P/2Dyl7jbgelamy7LihMCFiiySRlUoMCiGB6ZpciFS2eVSKRSPDkhm1CsFg0JCRRTBp4nOydChu6OzwOMPqN4T+y7V9GnVTOxlT6wvO9QpqNRGHD0r7/xjZ2dDe8DM5/CD8YcgUJXAi+YgNJhUV6K0EJcS0jujz0zdZqzh5qZRVSjXRhs8PkzYhK0P8QkaH+ISdD+EJOg/SEmQftDTOLS/nz9CfA9qhWVUsYLzud3HOvp4cSTPv77X6hwrIv7aiJqXNlf//Tt9dr6g1u/JjE93IlKKeOFRLnTJaXjraadi6Yk5tGtE6uQGpPIFAIWTubqyJEu29aFaiLTcJX/jUXeeHx36DUFlxwthQHlKiKSUmbkMsfzHzn6LBZbrRbfAJmy2WqlwZJ+8GlLSODCXqN2UX813H1+VT94cTxKKqJsjki4zP8WJ+Tc48hQtBRVriJAKQPmP3LEFWB9WvoG1WbrRYXvVhWhOAM9aEPaWZhJjawtsVUg43lhwOaIjLb93d2Sz5/3P4s/Th+5T/8BhjtR5SqaTSnTOz4ghVd2nydFbpTKCFQkI/Z8x+WqllHyyFf5KYUXjjmwcdOv1M0RJe71p+eHp1EPtx9wuBNVriJYKTOZ/4j5IVu0NyycLrYTcQ64rk9c6zPiot8bEyROFvL4GS8aW7wJdboVUugmwJqu358Vwd39rx0D9TDmXv+niJYiq0UIqJQhYP4jR3NaqB7cWiZWWvZIXNfH1DMtWnhJR6V3PaVIJFcfVC+Bwk6Zzd4hNhH3HGBNl+/PauDO/vzRwIDhTgANB6iUUeQ/GhXS625NGYIFVookxlzlUKEDFgJd5OHmyBTC9/zZeaOMNwBBJ3z25/7HFcjiCZ/9IcsE2h9iErQ/xCRof4hJ9Pc/rB+fE4/hn50sXv+CBAQ3/s9T3CGIxetfkIBg8vprUP9iFfJWdqyYbPHsDIwUM+e3YaVxY3+f31v6A08XYMP6l8EJ4emNhFLh4qrZYamOwEgxLk8QmQFt+3NmYDg/PO0/dnkpNq5/ye8WantM1NBr1EjVjhagESkG8QH9/Jf7n2KW1+vf/kWibgc2r39JlAsXpTbJXx1ktpcjWEUI0c9/+f3d4Vue/chjADaj+heBiCszyoiUhCLFpHEJOEf013/+pUAyqH+xGPONzj/GI8UgcyN8z59R/7JMhM/+UP+yTITP/pBlAu0PMQnaH2IStD/EJC7tz06B5FWLwH74uF04OEp1JO3L4kUxPPzyeHIQsa0shXqxAzXb+UXsmqMAzoylSUJkEFfxN/bf367zFEg+kEklSSadlF9YvChGpP+o8E05ehOdZgHsFaFe+OhNYf2jmlYAZyvyvb+TCyku9H+fyNMd93HvR9g+hv1XaR3IApbFB4XhNcimM3eVItSL99NHGC78X4z8ebj/nl19vQlQbR9TJTU7+IBpUUyb/rfN8jowCxyWQqFeEH9wEf/l8+fb9Z2dZ4StAg/P4z5IoIcfsGlRzLDWUa7RK9ivQKFe0AT9Qdv+4l+uP/hgH6/F+q5HHl4UN+l/rQt+ATUtimlb/+abhVrugGSqzJOCoV4SaVKzvga9BjVJFNC4w43+4Mna4b5QwDxYdy9FsC+Ru4WDveFy3agoRqQvakXICW9zkLwczWki1Av1uLRTKdkQmMAImYKH/IO+kElZ+dxsDIpixpyiM7fvzMmGli//kGnMPn/O8xxYUA5Bn0FRTEBZkf0PFMUElBWxPySgoP0hJkH7Q0yC9oeYxMXvL99/Hv7lORJHoPQvUlIk+wke6l/mhr7/e7BuxRy/Oz/83fsEAqR/IcM0XFzbwlLTsDLUv8wR/d//PrOO7vrXsUfPplaeTgD1L2NpkERqBtS/zBXX67/+79drG17ML4j6FxjUv8wPt/bX//N27Uu/JhEY/Qt8zUT9y/xwaX/c/KKeRg6i/gUA9S9zxWX+I2p+G1FvIwdP/0IcfrEVqdgOEfUvc8Rt/iNPKz8HQdK/EJVfRP3L3ED9C2KSFdn/QP1LQFkR+0MCCtofYhK0P8QkaH+ISfTtb5QAybc8NEbyH8lalSs4/ktqcq9EzFQSxSAu0LY/tu8rYr/0T/dP+75YoBGpi6xVycPxX0hzcEJKpGnVapdKBBbFoAnq4yb+RjTK/43GHngb26jURfXMcTL+iwNLl9VsslEgUQwaoDb68Q8ekf39fX7Iwr+4HzmQUhcCxX9hCP1Dtj4shUQxaH/aaNsfD3/F034w/anr9EcBlbrYTcfiv9hNSMmxDIBEMYg2+tffWCwuDqLRmIeBAyh1GeGI/zJW2rGsViGKQbTRv/7Grq3gL/wG2P3IpqUuslaFwPFfLAfaGlO0wKIYRBdP+Qc9YlbqAmhV4PgvCgcKimIQTcL3/BmlLstE+OwPpS7LRPjsD1km0P4Qk6D9ISZB+0NM4jL/DA8B44P+JVDxX5DFo69/OX1vbcD5o38JVvwXDVh4GAzz4hUP19/4xvqn0z6Jx122D1z8l266lqyQbPbsbELWJ49ul0Ra0pwQHfT33zae/mkLYJgE5o6QqLuhAxj/Jc8EgHSoDpeXiq1kcHQ6924a/Z93XPi/+MbOzgY/Oj88tbSA3ghS/JdsfZf3mUhlyNW00RE/cH/9vTs//Bj7yr0AYUnivyhH50PRnviJHBTwCuwKF/cfdgBUFogy7n7k4MV/YVfaFnV2rM3V6BAYPc/nXyARUU6L0Pjc4WL9Z199fSFI8V+cbfOOblRKFxTAeAfjvyAmWZH9DxTFBJQVsT8koKD9ISZB+0NMgvaHmGS6/YmHfZM6l/PDfR4ABvUvSqZPHhkyzf6E1GX906mz8O780AoAs+L6l6mMTR6VMmqm2V98g8mszj+NFfavY1+x6EMsEsc/Pt15GDpw+pfxqFbFbJZUhdVIo/NagFIGmDyolBGFjuBaK+sqva3//rrtUzt02TiA+hfS3rOjWrGVwW5eMXqi3AGUMuDkQaWMKHzBjtJZUqyuqPERr/b3wI7F4Y3g6F/y25lNK6oBU8JMG11SysCTV5GwtpWHO9erif7+7xrp33HN393dbSzqfuRg6l8cLzRyvPsp+pdx4MkTa1ITShlxSJ0l9dyrHDxwmv3Z97mE7H8e3u1G47HrtyIAjLf4a8HTv0y4RSutUQIYPQkrZeDJy0oZe5hMm7Spdz07S0YuV3QBOM3+4EgvPgaAIcHSv2ikP5pJKdOEqk8Ok1/tjWnUvyAmWZH9D9S/BJQVsT8koKD9ISZB+0NMgvaHmMSF/gUWxcwd9sT2MjQ7VfYNufuNXzt+9XJvHWvrX8DCRTAKyDwVUGwSPAWKuCFv5Kbu0amhJ2RtVFNDVqTLWQq09S9goQuEgO8kU9kcD6HSEEnY6plKZeQfZG8BK1CmiE3kWC2OzY6JfkWXxSIh29xopZoq/ct98pn7nJUktFHtUx8fZKodPmJ+u1jjm3vLibH1n1CQTApY8oTvykU2K/YLHNlbwAqUKWKTiUKnqoV9yrmGEHCNZXWrZLYVNcHR75XPjAaC3hFIaDPTc8uzy/bSGqDR+w+lgIXtUszwhkqxWmane0msxpT8br3G8mcRrmCxs7pZe2ZtqCakf2EvQ/IZRXNgSrLQJrU3Q/KmbHpJjY8Ytj9YwOIZMCzLRGEyTY5GhmDtQTMFy1G7Ob4fCNZUAclnZm0OCm0U/m+rQI7Ft7V3dZFJTXs3go22/gUsdAldIk0IWIbrp5YtFxnTJItFHKu7dQwqUPJwWBagsFxlJfZMaCkrZJnfHKVifKCmIlIMAeUzwEDQGZUhoY3KsSW20geO7Es6b3qw0Na/+Kp+KTQHnbGvNxhqBSxUKFCIIiyLXAgvraBSuUwVKWbWLhURZTRSKoUl+5Kx66/lQYQAeFXVl4jB+99QfH8Rb+D+G2IStD/EJGh/iEnQ/hCT6OtfhgGgWfznx17G9q4BgQmXUsZ+n5Zb56JCV/8ylv7o8Dz+7HHU9dgeNSBKVcuMShnvAy2EdontCtdrbt+lYKOrfxFl/OjRUxKP+j8jSC0iB3AZbB+BqhbJp/KCLJeqZOt1UqHdSNoSxyNIWcByv3zGodGRBiocJEGZjzwQUYVkaDJFQqPm+xsdCNyu/9hVmDrCuJ9zIQq1CAEDuOTBDESST803u/ULrmqp7kVq6e7g1XFur0t6x2BMGUDAokx1tG2ZOK3Z6OXL8EAqmQ8w0Er+RM+N/d2dH779GJuL/hlSi/SugAAuehSrzN+RbGHL3mhRRHUBBCwKele1zc1NMlFTHojAMh95IHVKpjCjbX9Mf0DWd3zcBHYCqUUSSSCAi4XrDESqqC6ygAUcyOGSuQObOhYo85EHQv83ASB1uTu/ZiUf93kEGBYAxvX9h0IDAslSFAFcZFUL0Gf1kpdEyMkJNYRkKdVNExaYpfuq8EISm0DxX8CBqCPLRBzNW6XUCdkEB6pnZJmPaiAI+3ce4ozC5hI19S8+Bn9RKDhAN6AK4DLZBdjnqD/rKG/VkesqfdBM8hl4oHbpQJL56MRjCPdG+bI8f17WAC4o85nOstjfsq6Owu29vLMs9oeEE7Q/xCRof4hJ0P4Qk5jMfzQv/QuIV1GMIgPJjDWl0T2fe0hEMdrxX6jx+ZX/yKv+RQsv4WP4vgtxBmSY1gFUUxrd47mHRhSjHf/F199fQsymf6lfbC4ofMxoB0IUF4eyA3meYE0NVzdz/JfQiGJc6w/+4tffuM/T0dC/LCp8DH+GtzXhFhVRXYCas7s61/Fflhk39mdtwnEBqkcJ9CRa+peghY/xuLvhOv7LMqNpf8z13X4lFn3R2ANP+d8gtPQviwwfM8M8vaIT/yU0aOpfqOt7erq/v89Lmfwl7npk7/qXRYWPGVvViZya8DyhmuBpEq/xX0IjitHPf0TvSnY2fBjZB/3LgsLHgBMF5wnUhE/Ta/yX0GwrL8vz50n9C+pKwsGy2N+kuwmNA1hxlsX+kHCC9oeYBO0PMQnaH2ISN/oX4tNPgJde/+JB1aKs6X/wmkArZbT1L+KFt9dr6w9uPY699PoXD6oWZU2/g9cEXCmjrX+xzfLx3eF8UnAtif7Fi6rlvor3zRPqc0mVMtrrP2F9cWqX/k9mefQv3lQtqrqzzjNEShlt+7u7JZ8/738Wf5w+8jkIzLLoX2ZHEWhGB2meIVLKaNvfcFP4/PA06nsEomXRv8yOKtCM732Gz/+pUx3ZMVAPY+71f0utf/Goapm5uWKe4VHK6OtfGH5oYJZa/+JR1TJ7c8U8Q6OUWZbnz6h/CSfLYn+ofwkny2J/SDhB+0NMgvaHmATtDzGJtv7F/vE58Rj+mSxUA6I7qcA9JwsrbvQvXuMO2XjVgMwhLVHA1SLhw4X+Zb7ATtFNWiKrDJSQLKlaJHy4Wf99fm/pD7xegCFApzhrWiJIGAJKSJZULRI+tO3PmYHh/PC0/3gOWZAkZk1LpBSbTEpIVjPZUADRtT96R/IpZnm9/u1fJOr/lCBmTEs0s9gE/V9A0NW/xDe+vzt8y7MfeQzApiEh0UhLJAtDkg2F1AUi4GqR8KGvf/ErBZKGhEQjLRHQq1rqMkuHyFzB58+ISdD+EJOg/SEmQftDTIL2h5gE7Q8xicv4L8NHg35pEQID6l8Wigv9CzPK23WeAil0oP5lwWjrX+7o3093PMS9dyCrWggcLUWO6rJ9xGvxX+NaLcQvc7WaO0H9iwlcrP9i5M/D/ffs6utR/wKoWhTRUoCoLvnBCaGN2KssKMfFVbMDB0ZRNcf93yDgIv7L58+36zs7zwhbBR6ex91bIKBqmRYtZTKqS363UNtjUgQWHK3a0WqO+peAoG1/8S/XH3ywj9difS+Dy6oWrWgpiXLhotQm+auDzLaQJKD+ZdnQj/8Sffxk7XBfKGAerHuQIkCqlunRUpxRXTgiWoxTEaPVXAb1LwvGTfwXnxQwsA+aOVoK3IdecwnUvywYfP6MmATtDzEJ2h9iErQ/xCRof4hJ0P4Qk+jqX+zIz4LQqV8UQKIYx+a1s9x+gnhfoSOg68Df6ORLhb7+5cG6FXP87vzw9znObO7MHD4GFMU4N68jpbawK2pnVuk9haLLQd5KcrK1siGEdfUv8Y1n1tFd/zr26JncanZkWUq6FgGzGjmcTbZYJGS7o6wJpU8CkiIRIHyMZlCYTErYTDKdtYtm/kmp6JIfbZ/YaUtWEdfrv/7v12sbnswPlKWAWY3apaTtbLghZraJCOoyWTMJpU9KgEmRgPAxWpvC+e1hoojR/h8ZfVOo5crX6rFCa45swqu7yefW/vp/3q596ccEpFxFclaj5NVFsdoUPsK5mSbXJED6JKKQz8hoiWJGCQnZdXwUEcSaIDf+4cIOLBRfpRXfYnZpf9z8or7OxEbOapRIZVpHbXodvLcmlD5pGhPhY7REMZm0bXGpjDhwhs2kF+WzyzbtHSwUSwJSH6z8brPL/EfU/Dai3kZWyVLkrEZMYHrkyIpk1wVqQumTVANBqY5AQFHMVvpgKLShRaLDzkkpMjEjsLDXOGAdVkQPq5zCxG3+I28rP4ZSliJlNSKqpRlQE6io1r/MqHYBq8G9gvOUC3UkOeEmWM+fZ89qhPmPwkGw7G92t4AOJBwEy/6QVQPtDzEJ2h9iErQ/xCT68V9GCZDmpn4JWv4jhVYFlLoQaWPDEegab9Yn0da/sH1fEfuFGudpfy4WOGP+o9nxJHWBtSqg1EVUTx4U6tlLZ7f4Q04VLvIfxaJR/m809sDDwNynOH6fa7sWOf+R2KoyJ3WBtSqKB0DCWMtXclIxBEI//sEjsr+/zw9Z+BfXA9NPtX7BP6QEl6fkroblE/mPjEtdLCStiqxqEdZH/7gabzqMCYIX4Am07Y+Hv+JpP5j+dDHpjwxLXYhCqyKrWq4uSKtlh58pbYvqzs22seQ5iJv731gsLg6i0ZjX0S+oIeVZisBaixSm+SOjUhdAq6JQtQwtjdpZyjIzap61tOX12pdnJDXrsCuBtv4lHru2gr/wIi9jbxVIUsS/ymaLZxV2Wd29gvIfGZW6gFoVUNViYfvWXJo7xXyzS0/KkspIAtRVR1v/4lf6IyKpQLg/UmUoMid1UfWpXELOEpMGsViC588odQkxS2B/6D1CzBLYHxJi0P4Qk6D9ISZB+0NM4iL/0TAETDCjv2ACo2VCX//CC9kG3Pz0Lx7ABEbLhQv9y+hlapp9Eo+7HdsRQapYbLWEGkZOYMSrkWz27OxsVKoZqwUJKPr6l42nf9oCGCaBuSMk6mrkXuPFQWEwYJFTmDEJhQGUwCghBDC0uMMrvDgm5TIm8AgHLu4/qFvc2eBH54enlhZQn97xASm8EscsgZbQXykTGGUtsQsLdsFqYgKjcOD+/vfu/PBj7CvXAoTEVoFwT0aIQ/+CCYxWDG39yygAKgtEGXc/sjNXUTZblAsZzKclrQ1gpjq9Gh0qwlJhAqOlQlv/Mrr6emakC2EaOaF/gcQijhKVPAaqiywBZp8/O35Y1sWr6Spi1v5wFbfqGLO///3P1MhIgMD9X8QkaH+ISdD+EJNMtb/hs75hzhmO/VwwmPoXT3zYjfzwmv5bfHPTfOJ8od/49uvLHycKQWavCdDefbj5Whq99W3kp4+Ts1pY4VyZYn9jSpfD8/izx1HCtz2sADCB1L945Mne4GaPfgySfCZefnczWxdyTWqRv6Te7d3/IPzD7iZ5M3j589jo/Vbu1++6N+8S5EPp4W77hvezsMJ5M8X+hPyFHz16SuJRcdy/jn31LCpK//HpzsvY9IS//olvVjwvPn/dev38hJ0zPfkfLP3Ly986xbioRtbXzz7ynx2vv+y+KybYN5XU33xR4e7KKiTWNzj78mXmp59YJ8/fDPboF3nUp11ChKOq8C6zz5+zR9t7iq+85BS5l1rPrn88+7hef0kq1GeICQDu0x76oWOedjUH/Nyp9dNWrZ/HXvnPr5kf3/Ff/T3Zfv4z/xX9AgvnzQzrP3YVpo4wDrz0122f2qG7kfuNf/1auLlh+hf2eazXmfFRm/iBvLlhHwM7/lej+K4cL3bedCM/kJObd7zCv45JsVx8d9J9uPnDFyc3N+xtoma3m2CGVXw3SNDefspYnYh+hn0y08m1mFm3d78++O63wbu4ZYhfqN9tySnm936r/8Gb//hL5Odk9+bfx9/+woIxAO7zSfPmt/SE/xPV3PDx8gNtbqpwDtxjfzzYX0y5znsQg8tnoP+fA/KdpX95snfy/Fuuf7m+/EhaPzwc6V9a/XKRjZF9+U/++cVTXwyD+wiT5RR/LH7b65En4tfB1HE6li/Xl+Tlrv1n/p8va79c04OrP55X98Ts2RVTf9PueZVO7APJfveN9k+SVf7v/pbracAmFlY4B+7TH5D1nfFN4Pga6d9xzd/d3W0s6nrg+DcFwj0ZYRfi2mtSYB5hLb2+Xn/3bjZr+FjZ/VAWF83Wz60vflTspKylSXsUKea6S5LfcDt+ffSBXvJcn4AWf/DLGXO01Gt2ijr+75vvyH/65Emcvk1Xf3yRWnDhvFHb3935NbvJ/SiivbBYa/z+IxqPXb8VAWA8xV+jXuff3+UePqyw4/Xsc7mQwRZSa63cD6/PyOtS4qbZ+3bz9UfyejfFPr/1LPkh8pDXY+uqJ44l3Wu6OrSdSrz8I4k8fGh3SQvjhF1D3xw9fDjKqcTWhWvDFSFdr7WsBSiRC6tdXvKQnLwhZz99XUr8liavN78lRfK6Ndk8zk7qOzaBihiFu3MY+/ZTNLcWkfFv0r9+zU+Hd2i9T4sqnDdq+1MFevEvAAxd2N0I3RVdpP9M9iYKhzhKnrwb2IdtQl3mTWfMjyiupPB6i67MbiZcJtgcKrwZ2P1ZPT8RdfZgH1wcTXsacDXwpBZWOGcM61/44y4iVmxaLVvCET6sDO98kWXEsP5lb+RI9JjRoyABx5j9/d//mRoZCRC4/4uYBO0PMQnaH2ISF/oXMCiMG+RUH4HA/+xLcEgaMH2SKqdSWNHWv4BBYdwhp/oIBH5nXwJD0lAjl9MngYXhRlv/ck9QGO9AWY2kSDH8/1keEyZbr5MKfdGKFjNqbrcWJSy/Ukq8Zr3g6DSbJVWengZ0yeOxFsa7ZUgjj9cFQ9IcH2SqHf7YMr9drFliE7Aw3HjTv/hOD8pqRORIMWWym75gmTwG1T2WXmPw6jhnJaDZHtpHrtHLU7vI8/xHL2hRPp0lRfvK2t6zfA2reWWlslG4ZMvCGrkceWV7KilOjfsf89npQ+4vDB3e9C++0wWyGvWuoEgxlGKVeR2SLWyN9j96V7XNzU1xnK3vWqV2WAVnpo78dmbTTssxqgmRb3ZEWK4L2jxhzVOOU5PacxuSJpsGKoGFoUNb/zJfoKxGiSQUKQbEEVOLe7VhMct6RMvp6j5H7CQODn91T1osO1ciNUOW2IheqcE4NTr+b6tAjnnuJ/qNucikphSGG239CxgUxg2OtLiOVEdQViMiR4ppl3jbCDk5IWeVZCnVTVN/lEt3q5mkI3wMCxSzfSTcUqbN01+dnSUjl46smBw2tnJK9P6BVbTdXfGEwHFqVOYLhqRJbKUPLO9rDU4UheFGW//im/pFkRUIXEVJkWKctayjvFVDap4flTgOIW8FTwle182e1AiuCLZfvUxJy/L8GSPFhJNlsT+MFBNOlsX+kHCC9oeYBO0PMQnaH2ISff2LIihMqMGcSvNCV/8Ci2Jc0mvk9lId15/poppjTqX5oat/gUUxbrCf6EXsx3rWtpikK2HIWhWoOZgpCe4Tao45lRaPW/2Ld1GMkKVMeCBIV0JArQrUHMyUBPcJNcdnjIvHjf5ljqIYRf6j2bUqcqYkdU6lSTCn0uLR1r/4LIq54CpLIVCh10BV/iOVVmWiOfg79Ck5lSaao/9bOJr6F4UoxiWJcoGpXSqEO5ryhNSFENv/tAGtCtS8B2dKUmhVgNFhMKfS/NDUv/gX/EUg6z0gCYhyYTZRN6HIlKSSlcyoNlk5UcoCwefPiEnQ/hCToP0hJkH7Q0yC9oeYBO0PMQnmP0JMoh3/hRpfiPMfIQvm/wE4emh/B2STRwAAAABJRU5ErkJggg==){width="213"
height="312"}

<span lang="zh-CN">主网络配置文件修改：</span>

![](data:image/png;base64,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){width="205"
height="302"}

<span lang="zh-CN">然后像上面那样启动</span>dacrs-d<span
lang="zh-CN">，再使用</span>rpc<span
lang="zh-CN">命令</span>registerapptx<span
lang="zh-CN">注册脚本。</span>

\

\

