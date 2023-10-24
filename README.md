## 上千行的代理规则，会对上网速度产生影响吗？
不会的。

我之前也认为这是一个每次网络数据包经过都会执行一次的规则文件，逐行匹配规则，所以需要尽可能精简。但后来和 SR 作者交流后发现这是一个误区，SR 在每次加载规则时都会生成一棵搜索树，可以理解为对主机名从后往前的有限状态机 DFA，并不是逐行匹配，并且对每次的匹配结果还有个哈希缓存。

换句话说，2000 行的规则和 50 行的规则在 SR 中均为同一量级的时间复杂度 O(1)。

## 广告过滤不完全？
该规则并不保证 100% 过滤所有的广告，尤其是视频广告，与网页广告不同的是，优酷等 App 每次升级都有可能更换一次广告策略，因此难以保证其广告屏蔽的实时有效性。

# 国内外划分 + 广告

国内外划分，对中国网站直连，外国网站代理。包含广告过滤。国外网站总是走代理，对于某些港澳台网站，速度反而会比直连更快。

规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_cnip_ad.conf

# 国内外划分
国内外划分，对中国网站直连，外国网站代理。不包含广告过滤。国外网站总是走代理，对于某些港澳台网站，速度反而会比直连更快。

规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_cnip.conf

# 黑名单过滤 + 广告
黑名单中包含了境外网站中无法访问的那些，对不确定的网站则默认直连。

代理：被墙的网站（GFWList）
直连：正常的网站
包含广告过滤
规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_banlist_ad.conf

# 白名单过滤 + 广告

白名单中包含了境外网站中可以访问的那些，对不确定的网站则默认代理。

直连：top500 网站中可直连的境外网站、中国网站
代理：默认代理其余的所有境外网站
包含广告过滤
规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_top500_whitelist_ad.conf

# 黑名单过滤

现在很多浏览器都自带了广告过滤功能，而广告过滤的规则其实较为臃肿，如果你不需要全局地过滤 App 内置广告和视频广告，可以选择这个不带广告过滤的版本。

代理：被墙的网站（GFWList）
直连：正常的网站
不包含广告过滤
规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_banlist.conf

# 白名单过滤

现在很多浏览器都自带了广告过滤功能，而广告过滤的规则其实较为臃肿，如果你不需要全局地过滤 App 内置广告和视频广告，可以选择这个不带广告过滤的版本。

直连：top500 网站中可直连的境外网站、中国网站
代理：默认代理其余的所有境外网站
不包含广告过滤
规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_top500_whitelist.conf

# 直连去广告

**如果你想将 SR 作为 iOS 全局去广告工具，这个规则会对你有所帮助。**

直连：所有请求
包含广告过滤
规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_direct_banad.conf

# 代理去广告

如果你想将 SR 作为 iOS 全局去广告 + 全局翻墙工具，这个规则会对你有所帮助。

直连：局域网请求
代理：其余所有请求
包含广告过滤
规则地址：

https://github.com/zhouzhouprogram/Shadowrocket-ADBlock-Rules/raw/master/sr_proxy_banad.conf
