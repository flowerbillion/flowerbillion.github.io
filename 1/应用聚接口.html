<?php
/**
 * 应用商店搜索引擎
 * 支持：小米、应用宝（新旧）、荣耀、努比亚、中兴、豌豆荚、三星
 * 豌豆荚支持历史版本查询
 * PHP 7.1+，需要 cURL 扩展
 */

// ------------------------------------------------------------
// API 入口
// ------------------------------------------------------------
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_SERVER['HTTP_X_REQUESTED_WITH']) && $_SERVER['HTTP_X_REQUESTED_WITH'] === 'XMLHttpRequest') {
    header('Content-Type: application/json');
    try {
        $action = isset($_POST['action']) ? $_POST['action'] : 'search';
        $deviceInfo = [
            'screenWidth' => isset($_POST['screenWidth']) ? (int)$_POST['screenWidth'] : 1080,
            'androidId'   => isset($_POST['androidId']) ? $_POST['androidId'] : '9774d56d682e549c',
            'sdkVersion'  => isset($_POST['sdkVersion']) ? (int)$_POST['sdkVersion'] : 29,
            'osRelease'   => isset($_POST['osRelease']) ? $_POST['osRelease'] : '10',
            'deviceModel' => isset($_POST['deviceModel']) ? $_POST['deviceModel'] : 'M2104K10AC'
        ];
        if ($action === 'search') {
            $store = trim($_POST['store']);
            $keyword = trim($_POST['keyword']);
            if (empty($store) || empty($keyword)) {
                throw new Exception('请选择商店并输入关键词');
            }
            $apps = StoreSearchEngine::search($deviceInfo, $store, $keyword, null);
            echo json_encode(['code' => 0, 'data' => $apps]);
        } elseif ($action === 'get_history') {
            $appId = trim($_POST['appId']);
            if (empty($appId)) {
                throw new Exception('缺少应用ID');
            }
            $history = StoreSearchEngine::getWdjHistory($appId, $deviceInfo, null);
            echo json_encode(['code' => 0, 'data' => $history]);
        } else {
            throw new Exception('未知操作');
        }
    } catch (Exception $e) {
        echo json_encode(['code' => -1, 'message' => $e->getMessage()]);
    }
    exit;
}
?>
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>应用商店搜索引擎</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
            background: #f5f7fb;
            margin: 0;
            padding: 20px;
            color: #1e293b;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        .card {
            background: white;
            border-radius: 20px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.05);
            padding: 24px 28px;
            margin-bottom: 30px;
        }
        h1 {
            font-size: 1.8rem;
            margin: 0 0 8px 0;
            font-weight: 600;
            background: linear-gradient(135deg, #1e3c72, #2b4c7c);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .sub {
            color: #5b6e8c;
            margin-bottom: 24px;
            border-left: 3px solid #3b82f6;
            padding-left: 12px;
        }
        .search-form {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: flex-end;
        }
        .form-group {
            flex: 1;
            min-width: 160px;
        }
        label {
            display: block;
            font-size: 0.85rem;
            font-weight: 500;
            margin-bottom: 6px;
            color: #334155;
        }
        select, input {
            width: 100%;
            padding: 10px 14px;
            font-size: 1rem;
            border: 1px solid #cbd5e1;
            border-radius: 14px;
            background: white;
            transition: 0.2s;
        }
        select:focus, input:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59,130,246,0.2);
        }
        button {
            background: #3b82f6;
            color: white;
            border: none;
            padding: 10px 24px;
            font-size: 1rem;
            font-weight: 500;
            border-radius: 40px;
            cursor: pointer;
            transition: 0.2s;
            margin-top: 22px;
            white-space: nowrap;
        }
        button:hover { background: #2563eb; transform: translateY(-1px); }
        button:active { transform: translateY(1px); }
        .loading {
            text-align: center;
            padding: 40px;
            color: #3b82f6;
            font-size: 1.1rem;
        }
        .results {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
            gap: 20px;
        }
        .app-card {
            background: white;
            border-radius: 24px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            overflow: hidden;
            transition: 0.2s;
            border: 1px solid #eef2f6;
            display: flex;
            flex-direction: column;
        }
        .app-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 24px rgba(0,0,0,0.1);
        }
        .app-header {
            display: flex;
            gap: 16px;
            padding: 20px 20px 12px 20px;
            align-items: center;
        }
        .app-icon {
            width: 64px;
            height: 64px;
            background: #f1f5f9;
            border-radius: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            flex-shrink: 0;
        }
        .app-icon img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .app-info {
            flex: 1;
        }
        .app-name {
            font-size: 1.2rem;
            font-weight: 600;
            margin-bottom: 4px;
        }
        .app-pkg {
            font-size: 0.75rem;
            color: #5b6e8c;
            font-family: monospace;
            word-break: break-all;
        }
        .app-meta {
            padding: 0 20px 12px 20px;
            font-size: 0.85rem;
            color: #334155;
            border-bottom: 1px solid #edf2f7;
        }
        .app-detail {
            padding: 16px 20px 20px 20px;
            font-size: 0.8rem;
            color: #475569;
            line-height: 1.5;
            background: #fafcff;
            white-space: pre-wrap;
            word-break: break-word;
            flex: 1;
        }
        .badge {
            background: #eef2ff;
            color: #1e40af;
            padding: 4px 10px;
            border-radius: 40px;
            font-size: 0.7rem;
            font-weight: 500;
            display: inline-block;
            margin-top: 6px;
        }
        .history-btn {
            background: #f0fdf4;
            color: #15803d;
            border: none;
            padding: 6px 12px;
            border-radius: 30px;
            font-size: 0.7rem;
            font-weight: 500;
            cursor: pointer;
            margin-top: 8px;
            width: auto;
            transition: 0.2s;
        }
        .history-btn:hover {
            background: #dcfce7;
            transform: none;
        }
        .empty {
            text-align: center;
            padding: 50px;
            background: white;
            border-radius: 28px;
            color: #5b6e8c;
        }
        footer {
            text-align: center;
            margin-top: 40px;
            color: #94a3b8;
            font-size: 0.75rem;
        }
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: white;
            border-radius: 28px;
            max-width: 500px;
            width: 90%;
            max-height: 80%;
            overflow-y: auto;
            padding: 20px;
            box-shadow: 0 20px 35px rgba(0,0,0,0.2);
        }
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #e2e8f0;
            padding-bottom: 12px;
            margin-bottom: 16px;
        }
        .modal-header h3 {
            margin: 0;
        }
        .close-modal {
            font-size: 28px;
            cursor: pointer;
        }
        .version-item {
            padding: 12px 0;
            border-bottom: 1px solid #f1f5f9;
        }
        .version-name {
            font-weight: 600;
        }
        .version-meta {
            font-size: 0.7rem;
            color: #5b6e8c;
            margin-top: 4px;
        }
        @media (max-width: 640px) {
            .card { padding: 18px; }
            .search-form { flex-direction: column; }
            button { width: 100%; margin-top: 8px; }
        }
    </style>
</head>
<body>
<div class="container">
    <div class="card">
        <h1>📱 应用商店搜索引擎</h1>
        <div class="sub">支持小米、应用宝（新旧）、荣耀、努比亚/中兴、豌豆荚、三星 · 豌豆荚支持历史版本</div>
        <form id="searchForm" class="search-form">
            <div class="form-group">
                <label>📦 选择商店</label>
                <select id="store" required>
                    <option value="小米">小米</option>
                    <option value="应用宝">应用宝</option>
                    <option value="旧应用宝">旧应用宝</option>
                    <option value="荣耀">荣耀</option>
                    <option value="努比亚">努比亚</option>
                    <option value="中兴">中兴</option>
                    <option value="豌豆荚">豌豆荚</option>
                    <option value="三星">三星</option>
                </select>
            </div>
            <div class="form-group">
                <label>🔍 应用关键词</label>
                <input type="text" id="keyword" placeholder="例如：微信、抖音、淘宝" required>
            </div>
            <button type="submit">🔎 搜索</button>
        </form>
    </div>

    <div id="resultsArea" class="results">
        <div class="empty">✨ 选择商店并输入关键词，开始搜索</div>
    </div>
    <footer>搜索结果来自各应用商店公开接口 · 豌豆荚历史版本点击卡片内按钮查看</footer>
</div>

<div id="historyModal" class="modal">
    <div class="modal-content">
        <div class="modal-header">
            <h3>历史版本</h3>
            <span class="close-modal">&times;</span>
        </div>
        <div id="historyList"></div>
    </div>
</div>

<script>
    const form = document.getElementById('searchForm');
    const resultsArea = document.getElementById('resultsArea');
    const modal = document.getElementById('historyModal');
    const historyListDiv = document.getElementById('historyList');
    const closeModal = document.querySelector('.close-modal');

    closeModal.onclick = () => modal.style.display = 'none';
    window.onclick = (e) => { if (e.target === modal) modal.style.display = 'none'; };

    form.addEventListener('submit', async (e) => {
        e.preventDefault();
        const store = document.getElementById('store').value;
        const keyword = document.getElementById('keyword').value.trim();
        if (!keyword) {
            alert('请输入关键词');
            return;
        }
        resultsArea.innerHTML = '<div class="loading">⏳ 正在搜索 ' + escapeHtml(store) + ' 商店的 “' + escapeHtml(keyword) + '” ...</div>';
        
        try {
            const formData = new FormData();
            formData.append('action', 'search');
            formData.append('store', store);
            formData.append('keyword', keyword);
            formData.append('screenWidth', window.screen.width);
            formData.append('androidId', '9774d56d682e549c');
            formData.append('sdkVersion', 29);
            formData.append('osRelease', '10');
            formData.append('deviceModel', 'M2104K10AC');
            const response = await fetch(window.location.href, {
                method: 'POST',
                headers: { 'X-Requested-With': 'XMLHttpRequest' },
                body: formData
            });
            const data = await response.json();
            if (data.code === 0) {
                renderResults(data.data, store);
            } else {
                resultsArea.innerHTML = '<div class="empty">❌ ' + escapeHtml(data.message || '搜索失败') + '</div>';
            }
        } catch (err) {
            resultsArea.innerHTML = '<div class="empty">⚠️ 网络错误：' + escapeHtml(err.message) + '</div>';
        }
    });

    function renderResults(apps, storeName) {
        if (!apps || apps.length === 0) {
            resultsArea.innerHTML = '<div class="empty">😞 未找到相关应用，试试其他关键词吧</div>';
            return;
        }
        const html = apps.map(app => `
            <div class="app-card">
                <div class="app-header">
                    <div class="app-icon">
                        ${app.iconUrl ? `<img src="${escapeHtml(app.iconUrl)}" onerror="this.src='data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2024%2024%22%20fill%3D%22%238c9eff%22%3E%3Cpath%20d%3D%22M12%202C6.48%202%202%206.48%202%2012s4.48%2010%2010%2010%2010-4.48%2010-10S17.52%202%2012%202zm-2%2015h-2v-2h2v2zm0-4h-2V7h2v6z%22%2F%3E%3C%2Fsvg%3E'">` : '<div style="background:#e2e8f0; width:100%; height:100%; border-radius:18px;"></div>'}
                    </div>
                    <div class="app-info">
                        <div class="app-name">${escapeHtml(app.name || '未知')}</div>
                        <div class="app-pkg">${escapeHtml(app.pkg || '')}</div>
                        <div class="badge">${escapeHtml(storeName)}</div>
                    </div>
                </div>
                <div class="app-meta">
                    📌 ${escapeHtml(app.subTitle || app.versionName || '')}
                </div>
                <div class="app-detail">
                    ${escapeHtml(app.detailText || '暂无详情')}
                    ${app.downloadUrl ? `<div style="margin-top: 12px;"><a href="${escapeHtml(app.downloadUrl)}" target="_blank" rel="noopener noreferrer" style="background:#eef2ff; padding:6px 12px; border-radius:40px; text-decoration:none; font-size:0.7rem; color:#2563eb;">⬇️ 下载链接</a></div>` : ''}
                    ${app.previewUrl ? `<div style="margin-top: 8px;"><a href="${escapeHtml(app.previewUrl)}" target="_blank" rel="noopener noreferrer" style="color:#3b82f6; font-size:0.7rem;">🔗 详情页</a></div>` : ''}
                    ${storeName === '豌豆荚' && app.appId ? `<button class="history-btn" data-appid="${escapeHtml(app.appId)}">📜 历史版本</button>` : ''}
                </div>
            </div>
        `).join('');
        resultsArea.innerHTML = html;

        document.querySelectorAll('.history-btn').forEach(btn => {
            btn.addEventListener('click', async (e) => {
                e.stopPropagation();
                const appId = btn.dataset.appid;
                if (!appId) return;
                await showHistory(appId);
            });
        });
    }

    async function showHistory(appId) {
        historyListDiv.innerHTML = '<div style="text-align:center">加载中...</div>';
        modal.style.display = 'flex';
        try {
            const formData = new FormData();
            formData.append('action', 'get_history');
            formData.append('appId', appId);
            formData.append('screenWidth', window.screen.width);
            formData.append('deviceModel', 'M2104K10AC');
            formData.append('osRelease', '10');
            const response = await fetch(window.location.href, {
                method: 'POST',
                headers: { 'X-Requested-With': 'XMLHttpRequest' },
                body: formData
            });
            const data = await response.json();
            if (data.code === 0 && data.data.length) {
                let html = '';
                data.data.forEach(ver => {
                    html += `
                        <div class="version-item">
                            <div class="version-name">${escapeHtml(ver.versionName)} (${ver.versionCode})</div>
                            <div class="version-meta">大小：${formatSize(ver.size)} | 更新：${formatDate(ver.updateTime)}</div>
                            ${ver.downloadUrl ? `<div style="margin-top:8px"><a href="${escapeHtml(ver.downloadUrl)}" target="_blank" rel="noopener noreferrer" style="font-size:0.7rem;">⬇️ 下载APK</a></div>` : ''}
                        </div>
                    `;
                });
                historyListDiv.innerHTML = html;
            } else {
                historyListDiv.innerHTML = '<div style="text-align:center">暂无历史版本</div>';
            }
        } catch (err) {
            historyListDiv.innerHTML = '<div style="text-align:center">加载失败</div>';
        }
    }

    function formatSize(bytes) {
        if (!bytes || bytes <= 0) return '未知';
        const mb = bytes / 1024 / 1024;
        return mb.toFixed(2) + ' MB';
    }
    function formatDate(timestamp) {
        if (!timestamp) return '未知';
        const d = new Date(timestamp);
        return d.toLocaleDateString();
    }
    function escapeHtml(str) {
        if (!str) return '';
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        });
    }
</script>
</body>
</html>

<?php
// ------------------------------------------------------------
// 后端核心类（修复版）
// ------------------------------------------------------------

class AppInfo {
    public $storeType = '';
    public $appId = '';
    public $name = '';
    public $pkg = '';
    public $author = '';
    public $versionName = '';
    public $versionCode = 0;
    public $subTitle = '';
    public $iconUrl = '';
    public $previewUrl = '';
    public $downloadUrl = '';
    public $detailText = '';
    public $xiaomi64Url = '';
    public $historyUrl = '';
}

class RequestToken {
    private $canceled = false;
    public function cancel() { $this->canceled = true; }
    public function isCanceled() { return $this->canceled; }
}

class StoreSearchException extends Exception {
    public $store;
    public function __construct($store, $message, Exception $previous = null) {
        $this->store = $store;
        parent::__construct($message, 0, $previous);
    }
}

class HttpUtil {
    public static function get($url, $token = null, $headers = []) {
        self::checkCanceled($token);
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
        curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
        curl_setopt($ch, CURLOPT_TIMEOUT, 30);
        if (!empty($headers)) curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
        $response = curl_exec($ch);
        $err = curl_error($ch);
        curl_close($ch);
        if ($err) throw new Exception("CURL GET error: " . $err);
        self::checkCanceled($token);
        return $response;
    }

    public static function postForm($url, $data, $token = null) {
        self::checkCanceled($token);
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_POST, true);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
        curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
        curl_setopt($ch, CURLOPT_TIMEOUT, 30);
        $response = curl_exec($ch);
        $err = curl_error($ch);
        curl_close($ch);
        if ($err) throw new Exception("CURL POST form error: " . $err);
        self::checkCanceled($token);
        return $response;
    }

    public static function postJson($url, $json, $token = null, $extraHeaders = []) {
        self::checkCanceled($token);
        $headers = array_merge(['Content-Type: application/json'], $extraHeaders);
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_POST, true);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $json);
        curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
        curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
        curl_setopt($ch, CURLOPT_TIMEOUT, 30);
        $response = curl_exec($ch);
        $err = curl_error($ch);
        curl_close($ch);
        if ($err) throw new Exception("CURL POST json error: " . $err);
        self::checkCanceled($token);
        return $response;
    }

    public static function post($url, $xml, $contentType, $token = null) {
        self::checkCanceled($token);
        $headers = ['Content-Type: ' . $contentType];
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_POST, true);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $xml);
        curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
        curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
        curl_setopt($ch, CURLOPT_TIMEOUT, 30);
        $response = curl_exec($ch);
        $err = curl_error($ch);
        curl_close($ch);
        if ($err) throw new Exception("CURL POST error: " . $err);
        self::checkCanceled($token);
        return $response;
    }

    public static function md5($str) { return md5($str); }
    public static function encode($str) { return urlencode($str); }
    public static function getFriendlyMessage(Exception $e, $defaultMsg) { return $e->getMessage() ?: $defaultMsg; }
    private static function checkCanceled($token) { if ($token && $token->isCanceled()) throw new RuntimeException("REQUEST_CANCELED"); }
}

class StoreSearchEngine {
    private function __construct() {}

    public static function search($deviceInfo, $store, $keyword, $token = null) {
        try {
            $trimmed = $keyword === null ? '' : trim($keyword);
            switch ($store) {
                case '小米': return self::searchXiaomi($trimmed, $token);
                case '旧应用宝': return self::searchYybOld($trimmed, $token);
                case '应用宝': return self::searchYybNew($trimmed, $token);
                case '荣耀': return self::searchHonor($trimmed, $token);
                case '努比亚': case '中兴': return self::searchNubiaOrZte($trimmed, $store, $token);
                case '豌豆荚': return self::searchWdj($deviceInfo, $trimmed, $token);
                case '三星': return self::searchSamsung($deviceInfo, $trimmed, $token);
                default: return [];
            }
        } catch (RuntimeException $e) {
            if ($e->getMessage() === 'REQUEST_CANCELED') throw $e;
            throw self::wrapStoreError($store, $e);
        } catch (Exception $e) {
            throw self::wrapStoreError($store, $e);
        }
    }

    // ---------- 小米 ----------
    private static function searchXiaomi($keyword, $token) {
        self::checkCanceled($token);
        $apps = [];
        $url = "https://app.market.xiaomi.com/apm/search?co=CN&densityScaleFactor=2.75&imei=d3964e30753e2ecc7d6138e661f571b9&la=zh&marketVersion=147&model=M2104K10AC&os=V12.5.16.0.RKPCNXM&page=0&ref=input&resolution=1080*2260&sdk=30&keyword=" . urlencode($keyword);
        $resp = HttpUtil::get($url, $token);
        self::checkCanceled($token);
        $json = json_decode($resp, true);
        $list = isset($json['listApp']) ? $json['listApp'] : [];
        foreach ($list as $item) {
            self::checkCanceled($token);
            try {
                $app = new AppInfo();
                $app->storeType = '小米';
                $app->appId = isset($item['appId']) ? (string)$item['appId'] : '';
                $app->name = isset($item['displayName']) ? $item['displayName'] : '';
                $app->pkg = isset($item['packageName']) ? $item['packageName'] : '';
                $app->author = isset($item['publisherName']) ? $item['publisherName'] : '';
                $app->versionName = isset($item['versionName']) ? $item['versionName'] : '';
                $app->versionCode = isset($item['versionCode']) ? (int)$item['versionCode'] : 0;
                $sub = isset($item['level2CategoryName']) ? $item['level2CategoryName'] : '';
                $app->subTitle = self::notEmpty($sub, $app->versionName);
                $icon = isset($item['icon']) ? $item['icon'] : '';
                $app->iconUrl = "https://file.market.xiaomi.com/mfc/thumbnail/png/w157q80/" . $icon;
                $app->previewUrl = "https://app.xiaomi.com/details?id=" . $app->pkg;
                $app->xiaomi64Url = "https://m.app.mi.com/details?id=" . $app->pkg;
                $size = isset($item['apkSize']) ? (int)$item['apkSize'] : 0;
                $createTime = isset($item['createTime']) ? (int)$item['createTime'] : 0;
                $updateTime = isset($item['updateTime']) ? (int)$item['updateTime'] : 0;
                $brief = isset($item['briefShow']) ? $item['briefShow'] : '';
                $app->detailText = "开发商：" . $app->author . "\n包名：" . $app->pkg . "\n版本：" . $app->versionName .
                    "\n大小：" . self::sizeText($size) . "\n上架时间：" . self::formatTime($createTime) .
                    "\n更新时间：" . self::formatTime($updateTime) . "\n简介：" . $brief;
                $apps[] = $app;
            } catch (Exception $e) {}
        }
        return $apps;
    }

    // ---------- 旧应用宝 ----------
    private static function searchYybOld($keyword, $token) {
        self::checkCanceled($token);
        $apps = [];
        $body = [
            'head' => ['cmd' => 'dynamicard3', 'authInfo' => ['businessId' => 'AuthName'], 'hostAppInfo' => ['scene' => 'search_result']],
            'body' => ['bid' => 'yybhome', 'listS' => ['keyword' => ['repStr' => [$keyword]]]]
        ];
        $resp = HttpUtil::postJson('https://yybadaccess.3g.qq.com/v2/dynamicard3', json_encode($body), $token);
        self::checkCanceled($token);
        $data = json_decode($resp, true);
        $components = isset($data['data']['components']) ? $data['data']['components'] : [];
        if (!empty($components)) {
            $itemData = isset($components[0]['data']['itemData']) ? $components[0]['data']['itemData'] : [];
            foreach ($itemData as $item) {
                self::checkCanceled($token);
                try {
                    $downloadUrl = isset($item['download_url']) ? $item['download_url'] : '';
                    $fixed = self::fixOldYybDownloadUrl($downloadUrl);
                    if (!empty($fixed)) {
                        $app = new AppInfo();
                        $app->storeType = '旧应用宝';
                        $app->name = isset($item['name']) ? $item['name'] : '';
                        $app->pkg = isset($item['pkg_name']) ? $item['pkg_name'] : '';
                        $app->author = isset($item['developer']) ? $item['developer'] : '';
                        $app->versionName = isset($item['version_name']) ? $item['version_name'] : '';
                        $app->subTitle = self::notEmpty(isset($item['editor_intro']) ? $item['editor_intro'] : '', $app->versionName);
                        $app->iconUrl = isset($item['icon']) ? $item['icon'] : '';
                        $app->previewUrl = "https://sj.qq.com/appdetail/" . $app->pkg;
                        $app->downloadUrl = $fixed;
                        $size = isset($item['apk_size']) ? (int)$item['apk_size'] : 0;
                        $update = isset($item['update_time']) ? (int)$item['update_time'] * 1000 : 0;
                        $intro = isset($item['editor_intro']) ? $item['editor_intro'] : '';
                        $app->detailText = "开发商：" . $app->author . "\n包名：" . $app->pkg . "\n版本：" . $app->versionName .
                            "\n大小：" . self::sizeText($size) . "\n更新时间：" . self::formatTime($update) . "\n简介：" . $intro;
                        $apps[] = $app;
                    }
                } catch (Exception $e) {}
            }
        }
        return $apps;
    }

    // ---------- 新应用宝 ----------
    private static function searchYybNew($keyword, $token) {
        self::checkCanceled($token);
        $apps = [];
        $body = ['body' => ['keyWord' => $keyword, 'pageSize' => 20]];
        $resp = HttpUtil::postJson('https://release.nj.qq.com/appstore/v1/getSearchInfo', json_encode($body), $token);
        self::checkCanceled($token);
        $data = json_decode($resp, true);
        $appList = isset($data['body']['data']['appList']) ? $data['body']['data']['appList'] : [];
        foreach ($appList as $item) {
            self::checkCanceled($token);
            try {
                $app = new AppInfo();
                $app->storeType = '应用宝';
                $app->name = isset($item['appName']) ? $item['appName'] : '';
                $app->pkg = isset($item['pkgName']) ? $item['pkgName'] : '';
                $app->author = isset($item['authorName']) ? $item['authorName'] : '';
                $app->versionName = isset($item['versionName']) ? $item['versionName'] : '';
                $app->versionCode = isset($item['versionCode']) ? (int)$item['versionCode'] : 0;
                $app->subTitle = self::notEmpty(isset($item['categoryName']) ? $item['categoryName'] : '', $app->versionName);
                $app->iconUrl = isset($item['iconUrl']) ? $item['iconUrl'] : '';
                $app->previewUrl = "https://sj.qq.com/appdetail/" . $app->pkg;
                $app->downloadUrl = isset($item['apkUrl']) ? $item['apkUrl'] : '';
                $size = isset($item['fileSize']) ? (int)$item['fileSize'] : 0;
                $intro = isset($item['editorIntro']) ? $item['editorIntro'] : '';
                $app->detailText = "开发商：" . $app->author . "\n包名：" . $app->pkg . "\n版本：" . $app->versionName .
                    " (" . $app->versionCode . ")\n大小：" . self::sizeText($size) . "\n简介：" . $intro;
                $apps[] = $app;
            } catch (Exception $e) {}
        }
        return $apps;
    }

    // ---------- 荣耀 ----------
    private static function searchHonor($keyword, $token) {
        self::checkCanceled($token);
        $apps = [];
        $body = [
            'key' => $keyword, 'pSize' => 16, 'start' => 0,
            'tInfo' => ['timestamp' => round(microtime(true) * 1000), 'cpu' => 'arm64-v8a', 'apkVer' => 0x09899fde]
        ];
        // 修复：补充有效的 User-Agent
        $headers = ['User-Agent: Dalvik/2.1.0 (Linux; U; Android 10; M2104K10AC Build/QKQ1.200830.002)', 'x-uuid: ' . self::uuid(), 'traceid: ' . self::uuid(), 'apkver: 160014302', 'areaid: CN'];
        $resp = HttpUtil::postJson('https://appmarket-api-drcn.hispace.hihonorcloud.com/market/searchapi/v2/app/list', json_encode($body), $token, $headers);
        self::checkCanceled($token);
        $data = json_decode($resp, true);
        $appLst = isset($data['data']['appLst']) ? $data['data']['appLst'] : [];
        foreach ($appLst as $item) {
            self::checkCanceled($token);
            try {
                $app = new AppInfo();
                $app->storeType = '荣耀';
                $app->name = isset($item['name']) ? $item['name'] : '';
                $app->pkg = isset($item['pName']) ? $item['pName'] : '';
                $app->author = isset($item['developer']) ? $item['developer'] : '';
                $app->versionName = isset($item['verName']) ? $item['verName'] : '';
                $app->versionCode = isset($item['verCode']) ? (int)$item['verCode'] : 0;
                $app->subTitle = self::notEmpty(isset($item['secondCategoryName']) ? $item['secondCategoryName'] : '', $app->versionName);
                $app->iconUrl = isset($item['imgUrl']) ? $item['imgUrl'] : '';
                $app->downloadUrl = isset($item['downUrl']) ? $item['downUrl'] : '';
                $size = isset($item['fileSize']) ? (int)$item['fileSize'] : 0;
                $update = isset($item['verUptTime']) ? $item['verUptTime'] : '';
                $brief = isset($item['brief']) ? $item['brief'] : '';
                $app->detailText = "包名：" . $app->pkg . "\n版本：" . $app->versionName . " (" . $app->versionCode .
                    ")\n更新时间：" . $update . "\n大小：" . self::sizeText($size) . "\n简介：" . $brief;
                $apps[] = $app;
            } catch (Exception $e) {}
        }
        return $apps;
    }

    // ---------- 努比亚/中兴 ----------
    private static function searchNubiaOrZte($keyword, $store, $token) {
        self::checkCanceled($token);
        $apps = [];
        $url = ($store == '努比亚') ? 'https://api-appstore.nubia.cn/Search/V3/GetSoftSearchList' : 'https://api-appstore.nubia.cn/Search/GetSoftSearchList';
        $time = time();
        $signBase = "Keyword=" . $keyword . "PageNo=1PageSize=10Time=" . $time . "GjWj8pc4bYq19NDkQ86fd6MtlW650Tki";
        $sign = md5($signBase);
        $postData = "Keyword=" . urlencode($keyword) . "&PageSize=10&Time=" . $time . "&PageNo=1&Sign=" . $sign;
        $resp = HttpUtil::postForm($url, $postData, $token);
        self::checkCanceled($token);
        $json = json_decode($resp, true);
        $dataList = isset($json['Data']) ? $json['Data'] : [];
        foreach ($dataList as $item) {
            self::checkCanceled($token);
            try {
                $softItem = isset($item['SoftItem']) ? $item['SoftItem'] : [];
                $app = new AppInfo();
                $app->storeType = $store;
                $app->name = isset($item['SoftName']) ? $item['SoftName'] : '';
                $app->pkg = isset($item['PackageName']) ? $item['PackageName'] : '';
                $app->subTitle = isset($item['Summary']) ? $item['Summary'] : '';
                if ($softItem) {
                    $app->versionName = isset($softItem['VersionName']) ? $softItem['VersionName'] : '';
                    $app->versionCode = isset($softItem['VersionCode']) ? (int)$softItem['VersionCode'] : 0;
                    $app->author = isset($softItem['BrandShowName']) ? $softItem['BrandShowName'] : '';
                    $app->downloadUrl = isset($softItem['MarketFileUrl']) ? $softItem['MarketFileUrl'] : '';
                    $app->previewUrl = isset($softItem['Wap']) ? $softItem['Wap'] : '';
                    $iconObj = isset($softItem['Icon']) ? $softItem['Icon'] : [];
                    $app->iconUrl = isset($iconObj['Px78']) ? $iconObj['Px78'] : '';
                }
                $author = isset($softItem['BrandShowName']) ? $softItem['BrandShowName'] : '';
                $versionStr = isset($softItem['VersionName']) ? $softItem['VersionName'] . '(' . $softItem['VersionCode'] . ')' : '';
                $size = isset($softItem['FileSize']) ? (int)$softItem['FileSize'] : 0;
                $pushTime = isset($softItem['PushTime']) ? (int)$softItem['PushTime'] : 0;
                $createTime = isset($item['CreateTime']) ? (int)$item['CreateTime'] * 1000 : 0;
                $summary = isset($item['Summary']) ? $item['Summary'] : '';
                $app->detailText = "来源：" . $author . "\n包名：" . $app->pkg . "\n上架时间：" . self::formatTime($createTime) .
                    "\n更新时间：" . self::formatTime($pushTime * 1000) . "\n版本：" . $versionStr . "\n大小：" . self::sizeText($size) .
                    "\n简介：" . $summary;
                $apps[] = $app;
            } catch (Exception $e) {}
        }
        return $apps;
    }

    // ---------- 豌豆荚（修复签名与 UA）----------
    private static function searchWdj($deviceInfo, $keyword, $token) {
        self::checkCanceled($token);
        $apps = [];

        $screenWidth = isset($deviceInfo['screenWidth']) ? (int)$deviceInfo['screenWidth'] : 1080;
        $osRelease   = isset($deviceInfo['osRelease'])   ? $deviceInfo['osRelease']   : '10';
        $deviceModel = isset($deviceInfo['deviceModel']) ? $deviceInfo['deviceModel'] : 'M2104K10AC';
        $androidId   = isset($deviceInfo['androidId'])   ? $deviceInfo['androidId']   : '9774d56d682e549c';

        // 关键修复：ua 不应 urlencode，应为原始字符串
        $ua = "(Android;N;AndroidOS{$osRelease};{$deviceModel})";

        $request1 = [
            'service' => 'search.app.list',
            'data' => [
                'rcount'      => 4,
                'screenWidth' => $screenWidth,
                's'           => '1',
                'functions'   => 'searchNotice,onlyShowNoDownload',
                'offset'      => 0,
                'pos'         => 'wdj/search/search_result_top/organic(豌豆荚)',
                'count'       => 10,
                'recommend'   => 1,
                'page'        => 1,
                'keyword'     => $keyword,
                'ua'          => $ua,
                'resourceType'=> 2
            ]
        ];
        $request2 = [
            'service' => 'op.ad.getAdsByKeyword',
            'data' => [
                'spaceId'     => 1289,
                'screenWidth' => $screenWidth,
                'offset'      => 0,
                'keyword'     => $keyword,
                'versionCode' => 0
            ]
        ];

        $jsonStr = self::buildWdjJsonString([$request1, $request2]);
        $sign = md5("-7200420523022531140secret.wdj.client" . $jsonStr . "LVJd97AbRtikeYRRhi3ocdwSD");

        $postData = [
            'id'      => -7200420523022531140,
            'encrypt' => 'md5',
            'sign'    => $sign,
            'client'  => [
                'caller'       => 'secret.wdj.client',
                'versionCode'  => 0,
                'umid'         => 'WV',
                'deviceModel'  => $deviceModel,
                'ex'           => [
                    'osVersion' => (int)$osRelease,
                    'productId' => 2011,
                    'net'       => 1,
                    'pos'       => 'wdj/search_result'
                ]
            ],
            'data'    => json_decode($jsonStr, true)
        ];

        $headers = [
            'User-Agent: wandoujia-client/8.6.0 (Linux; Android ' . $osRelease . '; ' . $deviceModel . ')',
            'X-Requested-With: XMLHttpRequest'
        ];
        $resp = HttpUtil::postJson('https://w-api.pp.cn/api/combine', json_encode($postData), $token, $headers);
        self::checkCanceled($token);

        $respData = json_decode($resp, true);
        if (!$respData || !isset($respData['data'][0]['data']['content'])) {
            $errMsg = isset($respData['msg']) ? $respData['msg'] : (json_last_error_msg() ?: '无数据');
            throw new Exception('豌豆荚接口异常：' . $errMsg);
        }

        $content = $respData['data'][0]['data']['content'];
        foreach ($content as $item) {
            self::checkCanceled($token);
            try {
                $app = new AppInfo();
                $app->storeType = '豌豆荚';
                $app->name      = isset($item['name']) ? $item['name'] : '';
                $app->pkg       = isset($item['packageName']) ? $item['packageName'] : '';
                $app->versionName = isset($item['versionName']) ? $item['versionName'] : '';
                $app->versionCode = isset($item['versionCode']) ? (int)$item['versionCode'] : 0;
                $app->subTitle  = self::notEmpty(isset($item['categoryName']) ? $item['categoryName'] : '', $app->versionName);
                $app->iconUrl   = isset($item['iconUrl']) ? $item['iconUrl'] : '';
                $app->downloadUrl = isset($item['downloadUrl']) ? $item['downloadUrl'] : '';
                $app->appId     = isset($item['id']) ? (string)$item['id'] : '';
                $app->previewUrl = "https://m.wandoujia.com/apps/" . $app->appId;
                $app->historyUrl = "https://m.wandoujia.com/apps/" . $app->appId . "/history";
                $size = isset($item['size']) ? (int)$item['size'] : 0;
                $update = isset($item['updateTime']) ? (int)$item['updateTime'] : 0;
                $intro = isset($item['editorRecommend']) ? $item['editorRecommend'] : '';
                $app->detailText = "版本：" . $app->versionName . " (" . $app->versionCode . ")\n大小：" . self::sizeText($size) .
                    "\n更新时间：" . self::formatDate($update) . "\n简介：" . $intro;
                $apps[] = $app;
            } catch (Exception $e) {}
        }
        return $apps;
    }

    private static function buildWdjJsonString($requests) {
        $parts = [];
        foreach ($requests as $req) {
            $service = $req['service'];
            $data = $req['data'];
            $dataJson = self::encodeDataMap($data);
            $parts[] = '{"service":"' . $service . '","data":' . $dataJson . '}';
        }
        return '[' . implode(',', $parts) . ']';
    }

    private static function encodeDataMap($map) {
        $pairs = [];
        foreach ($map as $k => $v) {
            if (is_string($v)) {
                $v = '"' . str_replace(['\\', '"'], ['\\\\', '\\"'], $v) . '"';
            } elseif (is_bool($v)) {
                $v = $v ? 'true' : 'false';
            } elseif (is_null($v)) {
                $v = 'null';
            } else {
                $v = (string)$v;
            }
            $pairs[] = '"' . $k . '":' . $v;
        }
        return '{' . implode(',', $pairs) . '}';
    }

    // 豌豆荚历史版本（修复 ID 不一致问题）
    public static function getWdjHistory($appId, $deviceInfo, $token = null) {
        self::checkCanceled($token);
        $osRelease   = isset($deviceInfo['osRelease'])   ? $deviceInfo['osRelease']   : '10';
        $deviceModel = isset($deviceInfo['deviceModel']) ? $deviceInfo['deviceModel'] : 'M2104K10AC';

        $historyReq = [
            [
                'service' => 'resource.app.getHistoryInfo',
                'data' => [
                    'packageName' => $appId,
                    'pageSize'    => 20,
                    'pageNo'      => 1
                ]
            ]
        ];
        $jsonStr = self::buildWdjJsonString($historyReq);
        // 关键修复：使用与搜索相同的 id 和 secret
        $sign = md5("-7200420523022531140secret.wdj.client" . $jsonStr . "LVJd97AbRtikeYRRhi3ocdwSD");

        $postData = [
            'id'      => -7200420523022531140,   // 修复：统一使用该 id
            'encrypt' => 'md5',
            'sign'    => $sign,
            'client'  => [
                'caller'       => 'secret.wdj.client',
                'versionCode'  => 21013,
                'versionName'  => '7.20.32',
                'deviceModel'  => $deviceModel,
                'ex'           => [
                    'osVersion' => (int)$osRelease,
                    'productId' => 2011,
                    'net'       => 1
                ]
            ],
            'data'    => json_decode($jsonStr, true)
        ];

        $headers = ['User-Agent: wandoujia-client/7.20.32 (Linux; Android ' . $osRelease . '; ' . $deviceModel . ')'];
        $resp = HttpUtil::postJson('https://w-api.pp.cn/api/resource.app.getHistoryInfo', json_encode($postData), $token, $headers);
        self::checkCanceled($token);

        $result = json_decode($resp, true);
        $historyList = [];
        if (isset($result['data'][0]['data']['list'])) {
            foreach ($result['data'][0]['data']['list'] as $item) {
                $historyList[] = [
                    'versionName' => isset($item['versionName']) ? $item['versionName'] : '',
                    'versionCode' => isset($item['versionCode']) ? $item['versionCode'] : 0,
                    'size'        => isset($item['size']) ? $item['size'] : 0,
                    'updateTime'  => isset($item['updateTime']) ? $item['updateTime'] : 0,
                    'downloadUrl' => isset($item['downloadUrl']) ? $item['downloadUrl'] : ''
                ];
            }
        }
        return $historyList;
    }

    // ---------- 三星 ----------
    private static function searchSamsung($deviceInfo, $keyword, $token) {
        self::checkCanceled($token);
        $apps = [];
        $androidId = isset($deviceInfo['androidId']) ? $deviceInfo['androidId'] : '';
        $sdk = isset($deviceInfo['sdkVersion']) ? $deviceInfo['sdkVersion'] : 29;
        $xml = '<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
                <SamsungProtocol openApiVersion="' . $sdk . '" deviceMakerType="1" mcc="460" mnc="15" csc="ETC" odcVersion="4.5.69.6" version="7.4" deviceFeature="locale=zh_CN_#Hans||abi64=arm64-v8a" userMode="0">
                <request name="searchProductListEx2Notc" id="2040" numParam="14" transactionId="25798663e028">
                <param name="imgWidth">135</param><param name="feedbackParam" /><param name="qlDomainCode">sa</param><param name="qlDeviceType">phone</param>
                <param name="extuk">' . self::xmlEscape($androidId) . '</param>
                <param name="stduk">188637ce76bdb6d326113dca9e3a90e4fc7ab47ddc32a6fce9ff4638511531db</param>
                <param name="qlInputMethod">iqry</param><param name="storeContentType">Apps</param>
                <param name="startNum">1</param><param name="imgHeight">135</param><param name="alignOrder">bestMatch</param>
                <param name="keyword">' . self::xmlEscape($keyword) . '</param>
                <param name="endNum">30</param><param name="contentType">all</param>
                </request></SamsungProtocol>';
        $response = HttpUtil::post('https://cn-ms.galaxyappstore.com/ods.as', $xml, 'application/xml; charset=UTF-8', $token);
        self::checkCanceled($token);
        $p = xml_parser_create();
        xml_parse_into_struct($p, $response, $vals, $index);
        xml_parser_free($p);
        $app = null;
        $dateStr = '';
        $sizeStr = '';
        foreach ($vals as $val) {
            self::checkCanceled($token);
            if ($val['tag'] == 'LIST') {
                if ($val['type'] == 'open') {
                    $app = new AppInfo();
                    $dateStr = '';
                    $sizeStr = '';
                } elseif ($val['type'] == 'close' && $app !== null) {
                    if (!empty($app->pkg)) {
                        $app->subTitle = $app->versionName . "(" . $app->versionCode . ")";
                        $app->previewUrl = "https://apps.galaxyappstore.com/detail/" . $app->pkg;
                        $dateStr = str_replace(';', '-', $dateStr);
                        if (substr($dateStr, -1) == '-') $dateStr = substr($dateStr, 0, -1);
                        $app->detailText = "应用包名：" . $app->pkg . "\n开发商：" . $app->author .
                            "\n当前版本：" . $app->versionName . "(" . $app->versionCode . ")\n大小：" . $sizeStr .
                            "\n上架日期：" . $dateStr;
                        $apps[] = $app;
                    }
                    $app = null;
                }
            } elseif ($val['tag'] == 'VALUE' && $app !== null && isset($val['attributes']['NAME'])) {
                $name = $val['attributes']['NAME'];
                $text = isset($val['value']) ? $val['value'] : '';
                switch ($name) {
                    case 'productName': $app->name = $text; break;
                    case 'GUID': $app->pkg = $text; break;
                    case 'productImgUrl': $app->iconUrl = $text; break;
                    case 'sellerName': $app->author = $text; break;
                    case 'version': $app->versionName = $text; break;
                    case 'versionCode': $app->versionCode = self::parseLong($text); break;
                    case 'realContentSize': $sizeStr = $text; break;
                    case 'date': $dateStr = $text; break;
                }
            }
        }
        return $apps;
    }

    // ---------- 公共辅助函数 ----------
    private static function fixOldYybDownloadUrl($url) {
        if (empty($url)) return '';
        try {
            // 尝试提取路径部分
            if (preg_match('/\/[^?]+\.apk/i', $url, $matches)) {
                $path = $matches[0];
                return 'https://imtt.dd.qq.com' . $path;
            }
            // 备选：直接替换域名
            return preg_replace('/^(http[s]?:\/\/)[^\/]+/', '$1imtt.dd.qq.com', $url);
        } catch (Exception $e) {
            return $url;
        }
    }

    private static function sizeText($bytes) { return $bytes <= 0 ? '未知大小' : sprintf("%.2f MB", $bytes / 1024 / 1024); }
    private static function formatTime($timestampMs) { return $timestampMs <= 0 ? '未知时间' : date('Y-m-d H:i:s', (int)($timestampMs / 1000)); }
    private static function formatDate($timestampMs) { return $timestampMs <= 0 ? '未知时间' : date('Y-m-d', (int)($timestampMs / 1000)); }
    private static function parseLong($str) { return is_numeric($str) ? (int)$str : 0; }
    private static function notEmpty($a, $b) { return !empty($a) ? $a : ($b !== null ? $b : ''); }
    private static function xmlEscape($str) { return str_replace(['&','<','>','"',"'"], ['&amp;','&lt;','&gt;','&quot;','&apos;'], $str ?: ''); }
    private static function checkCanceled($token) { if ($token && $token->isCanceled()) throw new RuntimeException('REQUEST_CANCELED'); }
    private static function wrapStoreError($store, Exception $e) { return new StoreSearchException($store, ($store ?: '当前商店') . '搜索失败：' . HttpUtil::getFriendlyMessage($e, '接口可能已变更'), $e); }
    private static function uuid() { return sprintf('%04x%04x-%04x-%04x-%04x-%04x%04x%04x', mt_rand(0,0xffff), mt_rand(0,0xffff), mt_rand(0,0xffff), mt_rand(0,0x0fff)|0x4000, mt_rand(0,0x3fff)|0x8000, mt_rand(0,0xffff), mt_rand(0,0xffff), mt_rand(0,0xffff)); }
}
?>