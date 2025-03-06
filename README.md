# WordPress Multisite Automation 

**一键部署高可用WordPress多站点环境，支持动态扩展与企业级安全策略**

## 📦 快速开始

### 环境要求
- Ubuntu 22.04 LTS
- 最小配置：2核CPU / 4GB内存 / 20GB硬盘

### 部署步骤
1. 克隆仓库：
   ```bash
   git clone https://github.com/hwc0212/wordpress-multisite-automation.git
   cd wordpress-multisite-automation
   ```

2. 初始化服务器环境：
   ```bash
   sudo bash setup_env.sh
   sudo reboot
   ```

3. 部署第一个站点：
   ```bash
   sudo bash add_site.sh example.com wp_db wp_user 'YourPassword123!'
   ```

## 🛠️ 功能特性
- **全隔离部署**：每个站点独立PHP进程、缓存及日志目录
- **性能优化**：内置FastCGI缓存 + Redis对象缓存加速
- **安全加固**：自动配置防火墙规则、Fail2Ban防御、SSL证书
- **监控支持**：集成Netdata实时监控（开箱即用）

## 🔧 配置调整指南
### 流量激增时优化
```nginx
# 修改Nginx连接数 (调整至CPU核心数×1024)
sudo nano /etc/nginx/nginx.conf
events {
  worker_connections 4096;
}
```

### 数据库性能调优
```bash
# 提升InnoDB缓冲池 (设置为物理内存70%)
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
innodb_buffer_pool_size = 8G
```

## 📊 监控与日志
- **实时仪表盘**：访问 `http://your-server-ip:19999` 查看Netdata
- **日志路径**：
  ```text
  /var/www/example.com/logs/      # 站点日志
  /var/log/mysql/slow.log         # 慢查询日志
  ```

## 🤝 参与贡献
1. Fork本仓库
2. 创建特性分支 (`git checkout -b feature/your-idea`)
3. 提交修改 (`git commit -am 'Add awesome feature'`)
4. 推送分支 (`git push origin feature/your-idea`)
5. 发起Pull Request

**遇到问题？**  
[提交Issue](https://github.com/hwc0212/wordpress-multisite-automation/issues) | 邮件支持：support@huwencai.com
