# aucklandtransport.github.io

!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AT-AC Transition Programme Workspace</title>
    
    <style>
      /* Theme variables */
      :root {
        --bg-primary: #ffffff;
        --bg-secondary: #f9fafb;
        --bg-tertiary: #f3f4f6;
        --bg-card: #ffffff;
        --text-primary: #1f2937;
        --text-secondary: #6b7280;
        --text-tertiary: #9ca3af;
        --border-primary: #e5e7eb;
        --border-secondary: #d1d5db;
        --shadow-sm: 0 2px 6px rgba(0,0,0,.06);
        --shadow-md: 0 4px 12px rgba(0,0,0,.1);
        --shadow-lg: 0 20px 50px rgba(0,0,0,.3);
      }
      
      [data-theme="dark"] {
        --bg-primary: #0f172a;
        --bg-secondary: #1e293b;
        --bg-tertiary: #334155;
        --bg-card: #1e293b;
        --text-primary: #f3f4f6;
        --text-secondary: #cbd5e1;
        --text-tertiary: #94a3b8;
        --border-primary: #334155;
        --border-secondary: #475569;
        --shadow-sm: 0 2px 6px rgba(0,0,0,.3);
        --shadow-md: 0 4px 12px rgba(0,0,0,.4);
        --shadow-lg: 0 20px 50px rgba(0,0,0,.6);
      }
      
      #atWorkspaceWrapper{background:transparent;padding:24px 0}
      #atWorkspace{max-width:1400px;margin:0 auto;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,sans-serif;color:var(--text-primary);line-height:1.4;transition:color 0.3s}
      #atWorkspace *{box-sizing:border-box}
      
      /* Sync status indicator */
      #atWorkspace .sync-status{position:fixed;top:10px;right:60px;padding:6px 12px;border-radius:20px;font-size:12px;z-index:1000;display:flex;align-items:center;gap:6px;background:#dcfce7;color:#15803d}
      [data-theme="dark"] #atWorkspace .sync-status{background:#064e3b;color:#6ee7b7}
      #atWorkspace .sync-dot{width:8px;height:8px;border-radius:50%;background:currentColor;animation:pulse 2s infinite}
      @keyframes pulse{0%{opacity:1}50%{opacity:0.5}100%{opacity:1}}
      
      /* Theme toggle button */
      #atWorkspace .theme-toggle-global{position:fixed;top:10px;right:10px;width:40px;height:40px;border-radius:50%;background:var(--bg-card);border:2px solid var(--border-primary);cursor:pointer;display:flex;align-items:center;justify-content:center;z-index:1000;transition:all 0.3s;box-shadow:var(--shadow-sm)}
      #atWorkspace .theme-toggle-global:hover{transform:scale(1.1);box-shadow:var(--shadow-md)}
      #atWorkspace .theme-toggle-global .icon{font-size:20px;transition:transform 0.3s}
      #atWorkspace .theme-toggle-global:hover .icon{transform:rotate(180deg)}
      
      /* header & nav */
      #atWorkspace header{background:linear-gradient(135deg, #1e3a8a 0%, #dc2626 100%);border-radius:12px;padding:20px 30px;display:flex;align-items:center;gap:10px;box-shadow:var(--shadow-md);justify-content:space-between;color:white}
      #atWorkspace header h1{margin:0;font-size:1.8rem;font-weight:700}
      #atWorkspace header .subtitle{font-size:0.9rem;opacity:0.9;margin-top:4px}
      #atWorkspace header .btn{background:rgba(255,255,255,0.2);color:white;border:1px solid rgba(255,255,255,0.3)}
      #atWorkspace header .btn:hover{background:rgba(255,255,255,0.3)}
      #atWorkspace .vault-btn{position:relative;padding-right:40px}
      #atWorkspace .vault-badge{position:absolute;top:-8px;right:-8px;background:#dc2626;color:#fff;font-size:0.75rem;font-weight:700;padding:2px 8px;border-radius:20px;min-width:24px;text-align:center}
      
      #atWorkspace nav{background:var(--bg-card);border-radius:12px;margin:22px 0;display:flex;justify-content:space-around;box-shadow:var(--shadow-sm);border:1px solid var(--border-primary)}
      #atWorkspace .tab{flex:1;text-align:center;padding:14px 8px;cursor:pointer;font-size:1rem;border-bottom:4px solid transparent;transition:all 0.2s;position:relative;color:var(--text-primary)}
      #atWorkspace .tab:hover{background:var(--bg-secondary)}
      #atWorkspace .tab.active{border-bottom-color:#2563eb;background:var(--bg-secondary);font-weight:700}
      #atWorkspace .tab.active::after{content:'';position:absolute;bottom:-4px;left:0;right:0;height:4px;background:linear-gradient(90deg, #3b82f6 0%, #dc2626 100%)}
      
      /* panels */
      #atWorkspace .panel{display:none}
      #atWorkspace .panel.active{display:block}
      #atWorkspace .panel-header{display:flex;justify-content:space-between;align-items:center;margin:28px 0 18px}
      #atWorkspace .panel-header h2{margin:0;color:var(--text-primary);font-size:1.5rem}
      #atWorkspace .add-btn{background:linear-gradient(135deg, #10b981 0%, #059669 100%);color:#fff;border:none;padding:10px 18px;border-radius:8px;font-size:.9rem;cursor:pointer;transition:all 0.2s;box-shadow:0 2px 6px rgba(16, 185, 129, 0.2)}
      #atWorkspace .add-btn:hover{transform:translateY(-1px);box-shadow:0 4px 12px rgba(16, 185, 129, 0.3)}
      #atWorkspace .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(380px,1fr));gap:28px}
      
      /* card - default theme */
      #atWorkspace .card{background:var(--bg-card);border-radius:14px;padding:24px;padding-top:50px;display:flex;flex-direction:column;gap:12px;position:relative;box-shadow:var(--shadow-sm);transition:transform 0.2s,box-shadow 0.2s;border:1px solid var(--border-primary);min-height:200px}
      #atWorkspace .card:hover{transform:translateY(-2px);box-shadow:var(--shadow-md);border-color:#ddd6fe}
      [data-theme="dark"] #atWorkspace .card:hover{border-color:#6366f1}
      #atWorkspace .card h3{margin:0;font-size:1.1rem;color:var(--text-primary);word-wrap:break-word;padding-right:90px}
      #atWorkspace .card p{margin:0;color:var(--text-secondary);font-size:.9rem;line-height:1.5}
      
      /* card - dark theme */
      #atWorkspace .card.dark-theme{background:#1e293b;color:#e5e7eb;border:1px solid #334155}
      #atWorkspace .card.dark-theme h3{color:#f3f4f6}
      #atWorkspace .card.dark-theme p{color:#cbd5e1}
      #atWorkspace .card.dark-theme .link-list a{color:#60a5fa}
      #atWorkspace .card.dark-theme .file-item{background:#0f172a;color:#e5e7eb;border:1px solid #334155}
      #atWorkspace .card.dark-theme .file-item:hover{background:#334155}
      #atWorkspace .card.dark-theme .vault-status{background:#1e3a8a;color:#93c5fd}
      
      /* Priority indicators */
      #atWorkspace .priority-badge{position:absolute;top:12px;left:12px;padding:6px 12px;border-radius:6px;font-size:0.75rem;font-weight:600;z-index:10}
      #atWorkspace .priority-high{background:#fee2e2;color:#dc2626}
      #atWorkspace .priority-medium{background:#fef3c7;color:#92400e}
      #atWorkspace .priority-low{background:#dcfce7;color:#15803d}
      #atWorkspace .card.dark-theme .priority-high{background:#dc2626;color:#fff}
      #atWorkspace .card.dark-theme .priority-medium{background:#f59e0b;color:#fff}
      #atWorkspace .card.dark-theme .priority-low{background:#10b981;color:#fff}
      
      /* theme toggle button */
      #atWorkspace .theme-toggle{position:absolute;top:12px;right:50px;background:#f3f4f6;border:none;width:36px;height:36px;border-radius:8px;cursor:pointer;font-size:18px;transition:all 0.2s;display:flex;align-items:center;justify-content:center;z-index:10}
      #atWorkspace .theme-toggle:hover{background:#e5e7eb}
      #atWorkspace .card.dark-theme .theme-toggle{background:#475569;color:#fff}
      #atWorkspace .card.dark-theme .theme-toggle:hover{background:#64748b}
      
      #atWorkspace .del{position:absolute;top:12px;right:12px;background:#fee2e2;border:none;width:36px;height:36px;border-radius:8px;color:#dc2626;cursor:pointer;font-size:1.1rem;transition:background 0.2s;display:flex;align-items:center;justify-content:center;z-index:10}
      #atWorkspace .del:hover{background:#fecaca}
      #atWorkspace .card.dark-theme .del{background:#dc2626;color:#fff}
      #atWorkspace .card.dark-theme .del:hover{background:#ef4444}
      
      #atWorkspace .actions{display:flex;flex-wrap:wrap;gap:8px;margin-top:auto}
      #atWorkspace .pill{border:none;border-radius:6px;padding:8px 14px;font-size:.8rem;cursor:pointer;transition:all 0.2s;font-weight:500}
      #atWorkspace .blue{background:#e0e7ff;color:#3730a3}
      #atWorkspace .blue:hover{background:#c7d2fe}
      #atWorkspace .green{background:#dcfce7;color:#15803d}
      #atWorkspace .green:hover{background:#bbf7d0}
      #atWorkspace .yellow{background:#fef9c3;color:#92400e}
      #atWorkspace .yellow:hover{background:#fef3c7}
      #atWorkspace .gray{background:#f3f4f6;color:#374151}
      #atWorkspace .gray:hover{background:#e5e7eb}
      #atWorkspace .red{background:#fee2e2;color:#dc2626}
      #atWorkspace .red:hover{background:#fecaca}
      #atWorkspace .purple{background:#ede9fe;color:#6b21a8}
      #atWorkspace .purple:hover{background:#ddd6fe}
      
      /* Dark theme pills */
      #atWorkspace .card.dark-theme .blue{background:#3730a3;color:#e0e7ff}
      #atWorkspace .card.dark-theme .blue:hover{background:#4c1d95}
      #atWorkspace .card.dark-theme .green{background:#15803d;color:#dcfce7}
      #atWorkspace .card.dark-theme .green:hover{background:#166534}
      #atWorkspace .card.dark-theme .yellow{background:#92400e;color:#fef3c7}
      #atWorkspace .card.dark-theme .yellow:hover{background:#78350f}
      #atWorkspace .card.dark-theme .gray{background:#475569;color:#e5e7eb}
      #atWorkspace .card.dark-theme .gray:hover{background:#64748b}
      #atWorkspace .card.dark-theme .red{background:#dc2626;color:#fff}
      #atWorkspace .card.dark-theme .red:hover{background:#ef4444}
      #atWorkspace .card.dark-theme .purple{background:#6b21a8;color:#ede9fe}
      #atWorkspace .card.dark-theme .purple:hover{background:#7c3aed}
      
      #atWorkspace .pill:disabled{opacity:.5;cursor:not-allowed}
      #atWorkspace .link-list{margin-top:10px;padding:10px;background:#f9fafb;border-radius:8px}
      #atWorkspace .card.dark-theme .link-list{background:rgba(0,0,0,0.3)}
      #atWorkspace .link-list a{display:block;color:#2563eb;font-size:.85rem;text-decoration:none;word-break:break-all;margin-bottom:6px;padding:4px 0}
      #atWorkspace .link-list a:hover{text-decoration:underline}
      #atWorkspace .link-list a:last-child{margin-bottom:0}
      
      /* File list styling */
      #atWorkspace .file-list{margin-top:12px;border-top:1px solid #e5e7eb;padding-top:12px}
      #atWorkspace .card.dark-theme .file-list{border-top-color:#475569}
      #atWorkspace .file-item{display:flex;align-items:center;justify-content:space-between;padding:10px;margin-bottom:8px;background:#f9fafb;border-radius:8px;font-size:.85rem;gap:10px}
      #atWorkspace .file-item:hover{background:#f3f4f6}
      #atWorkspace .file-info{display:flex;align-items:center;gap:8px;flex:1;min-width:0}
      #atWorkspace .file-info span{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
      #atWorkspace .file-actions{display:flex;gap:6px;flex-shrink:0}
      #atWorkspace .vault-status{font-size:.7rem;padding:3px 8px;border-radius:4px;background:#e0e7ff;color:#3730a3;white-space:nowrap}
      
      /* Status tags */
      #atWorkspace .status-tags{display:flex;gap:6px;margin-top:8px;flex-wrap:wrap}
      #atWorkspace .status-tag{font-size:0.75rem;padding:4px 10px;border-radius:6px;font-weight:600}
      #atWorkspace .tag-at{background:#fee2e2;color:#dc2626}
      #atWorkspace .tag-ac{background:#dbeafe;color:#1e40af}
      #atWorkspace .tag-integrated{background:#ede9fe;color:#6b21a8}
      #atWorkspace .card.dark-theme .tag-at{background:#dc2626;color:#fff}
      #atWorkspace .card.dark-theme .tag-ac{background:#2563eb;color:#fff}
      #atWorkspace .card.dark-theme .tag-integrated{background:#7c3aed;color:#fff}
      
      /* Modal styles */
      #atWorkspace .overlay{position:fixed;inset:0;background:rgba(0,0,0,.45);display:flex;align-items:center;justify-content:center;visibility:hidden;opacity:0;transition:.2s;z-index:1000}
      [data-theme="dark"] #atWorkspace .overlay{background:rgba(0,0,0,.7)}
      #atWorkspace .overlay.show{visibility:visible;opacity:1}
      #atWorkspace #vaultOverlay{z-index:1100}
      #atWorkspace .modal{background:var(--bg-card);border-radius:12px;width:90%;max-width:600px;padding:26px;display:flex;flex-direction:column;gap:14px;max-height:92vh;overflow:auto;border:1px solid var(--border-primary)}
      #atWorkspace .modal h3{margin:0;color:var(--text-primary)}
      #atWorkspace .modal input,#atWorkspace .modal textarea,#atWorkspace .modal select{border:1px solid var(--border-secondary);border-radius:6px;padding:8px 12px;font-size:.9rem;width:100%;background:var(--bg-primary);color:var(--text-primary)}
      #atWorkspace .modal input:focus,#atWorkspace .modal textarea:focus,#atWorkspace .modal select:focus{outline:none;border-color:#2563eb;box-shadow:0 0 0 2px rgba(37,99,235,.1)}
      #atWorkspace .btn{background:var(--bg-tertiary);color:var(--text-primary);border:none;padding:8px 16px;border-radius:6px;cursor:pointer;font-size:.9rem;transition:background 0.2s}
      #atWorkspace .btn:hover{background:var(--border-primary)}
      [data-theme="dark"] #atWorkspace .btn:hover{background:var(--border-secondary)}
      #atWorkspace .btn:disabled{opacity:0.5;cursor:not-allowed}
      #atWorkspace .btn:disabled:hover{background:var(--bg-tertiary)}
      
      /* Priority selector */
      #atWorkspace .priority-selector{display:flex;gap:8px;margin-top:8px}
      #atWorkspace .priority-option{flex:1;padding:8px;border:2px solid var(--border-primary);border-radius:6px;text-align:center;cursor:pointer;transition:all 0.2s;background:var(--bg-primary);color:var(--text-primary)}
      #atWorkspace .priority-option:hover{border-color:#ddd6fe}
      [data-theme="dark"] #atWorkspace .priority-option:hover{border-color:#6366f1}
      #atWorkspace .priority-option.selected{border-color:#2563eb;background:#eff6ff}
      [data-theme="dark"] #atWorkspace .priority-option.selected{background:#1e3a8a}
      
      /* Notification */
      #atWorkspace .notification{position:fixed;top:60px;right:20px;background:#10b981;color:#fff;padding:12px 20px;border-radius:8px;box-shadow:0 4px 12px rgba(0,0,0,.15);opacity:0;transform:translateY(-20px);transition:all 0.3s;z-index:1200}
      #atWorkspace .notification.show{opacity:1;transform:translateY(0)}
      
      /* Quick stats bar */
      #atWorkspace .stats-bar{background:var(--bg-secondary);border-radius:8px;padding:16px;margin-bottom:20px;display:grid;grid-template-columns:repeat(auto-fit, minmax(150px, 1fr));gap:16px;border:1px solid var(--border-primary)}
      #atWorkspace .stat-item{text-align:center}
      #atWorkspace .stat-value{font-size:1.8rem;font-weight:700;color:var(--text-primary)}
      #atWorkspace .stat-label{font-size:0.8rem;color:var(--text-secondary)}
      
      /* Vault Modal - Full Size */
      #atWorkspace .vault-modal{background:var(--bg-primary);border-radius:0;width:100%;height:100vh;max-width:100%;max-height:100vh;display:flex;flex-direction:column;box-shadow:none;margin:0}
      #atWorkspace .vault-header{background:linear-gradient(135deg, #1e3a8a 0%, #dc2626 100%);color:#fff;padding:24px;border-radius:0;display:flex;justify-content:space-between;align-items:center}
      #atWorkspace .vault-header h2{margin:0;font-size:1.5rem}
      #atWorkspace .vault-close{background:rgba(255,255,255,0.2);border:none;color:#fff;width:36px;height:36px;border-radius:8px;font-size:24px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:background 0.2s}
      #atWorkspace .vault-close:hover{background:rgba(255,255,255,0.3)}
      
      /* Category Management - Full Size Adjustments */
      #atWorkspace .category-bar{background:var(--bg-secondary);padding:16px 24px;display:flex;align-items:center;gap:16px;flex-wrap:wrap;border-bottom:1px solid var(--border-primary)}
      #atWorkspace .category-tabs{display:flex;gap:10px;flex:1;flex-wrap:wrap;align-items:center}
      #atWorkspace .category-tab{padding:8px 16px;background:var(--bg-card);border:2px solid transparent;border-radius:20px;cursor:pointer;transition:all 0.3s;display:flex;align-items:center;gap:8px;font-weight:500;color:var(--text-primary);font-size:0.9rem;position:relative}
      #atWorkspace .category-tab:hover{background:var(--bg-tertiary);border-color:#2563eb}
      #atWorkspace .category-tab.active{background:#2563eb;color:white;border-color:#2563eb}
      #atWorkspace .category-color{width:12px;height:12px;border-radius:50%}
      #atWorkspace .category-menu-btn{position:absolute;right:8px;top:50%;transform:translateY(-50%);background:transparent;border:none;color:inherit;font-size:16px;cursor:pointer;padding:0 4px;opacity:0;transition:opacity 0.2s}
      #atWorkspace .category-tab:hover .category-menu-btn{opacity:1}
      #atWorkspace .category-tab.active .category-menu-btn{opacity:1}
      #atWorkspace .add-category-btn{padding:8px 16px;background:#10b981;color:white;border:none;border-radius:20px;cursor:pointer;font-weight:500;transition:all 0.3s;display:flex;align-items:center;gap:5px;font-size:0.9rem}
      #atWorkspace .add-category-btn:hover{background:#059669;transform:translateY(-2px)}
      
      /* Category Menu Dropdown */
      #atWorkspace .category-menu{position:absolute;top:100%;right:0;margin-top:4px;background:var(--bg-card);border:1px solid var(--border-primary);border-radius:8px;box-shadow:var(--shadow-md);z-index:100;min-width:120px;display:none}
      #atWorkspace .category-menu.show{display:block}
      #atWorkspace .category-menu-item{padding:8px 16px;cursor:pointer;font-size:0.85rem;color:var(--text-primary);transition:background 0.2s}
      #atWorkspace .category-menu-item:hover{background:var(--bg-secondary)}
      #atWorkspace .category-menu-item.delete{color:#dc2626}
      
      /* Edit Category Modal */
      #atWorkspace #editCategoryOverlay{z-index:1150}
      
      /* Category Modal */
      #atWorkspace .category-modal{background:var(--bg-card);border-radius:12px;width:90%;max-width:500px;padding:30px;border:1px solid var(--border-primary)}
      #atWorkspace .category-modal h3{margin:0 0 20px 0;color:var(--text-primary);font-size:20px}
      #atWorkspace .modal-form{display:flex;flex-direction:column;gap:15px}
      #atWorkspace .modal-form label{color:var(--text-secondary);font-weight:500}
      #atWorkspace .modal-form input{padding:10px;border:2px solid var(--border-primary);border-radius:6px;font-size:15px;background:var(--bg-secondary);color:var(--text-primary)}
      #atWorkspace .modal-form input:focus{outline:none;border-color:#2563eb}
      #atWorkspace .color-picker{display:flex;gap:10px;flex-wrap:wrap}
      #atWorkspace .color-option{width:40px;height:40px;border-radius:50%;cursor:pointer;border:3px solid transparent;transition:all 0.3s}
      #atWorkspace .color-option:hover{transform:scale(1.1)}
      #atWorkspace .color-option.selected{border-color:#2563eb;box-shadow:0 0 0 2px var(--bg-card), 0 0 0 4px #2563eb}
      #atWorkspace .modal-actions{display:flex;gap:10px;margin-top:20px;justify-content:flex-end}
      #atWorkspace .modal-btn{padding:10px 20px;border:none;border-radius:6px;cursor:pointer;font-weight:500;transition:all 0.3s}
      #atWorkspace .modal-btn.primary{background:#2563eb;color:white}
      #atWorkspace .modal-btn.primary:hover{background:#1d4ed8}
      #atWorkspace .modal-btn.secondary{background:#6b7280;color:white}
      #atWorkspace .modal-btn.secondary:hover{background:#4b5563}
      
      /* Document Preview Modal - Higher z-index */
      #atWorkspace #previewOverlay{z-index:1200}
      #atWorkspace .preview-modal{background:var(--bg-card);border-radius:16px;width:90%;max-width:1000px;max-height:90vh;display:flex;flex-direction:column;box-shadow:var(--shadow-lg);border:1px solid var(--border-primary)}
      #atWorkspace .preview-header{background:#1f2937;color:#fff;padding:16px 24px;border-radius:16px 16px 0 0;display:flex;justify-content:space-between;align-items:center}
      [data-theme="dark"] #atWorkspace .preview-header{background:#0f172a}
      #atWorkspace .preview-header h3{margin:0;font-size:1.2rem}
      #atWorkspace .preview-content{flex:1;overflow:auto;padding:24px;background:var(--bg-secondary)}
      #atWorkspace .preview-iframe{width:100%;height:600px;border:1px solid var(--border-primary);border-radius:8px;background:var(--bg-card)}
      #atWorkspace .preview-text{white-space:pre-wrap;font-family:monospace;font-size:14px;line-height:1.6;background:var(--bg-card);padding:20px;border-radius:8px;border:1px solid var(--border-primary);color:var(--text-primary)}
      
      /* Category Selection Modal */
      #atWorkspace #categorySelectOverlay{z-index:1150}
      #atWorkspace .category-select-modal{background:var(--bg-card);border-radius:12px;width:90%;max-width:400px;padding:24px;border:1px solid var(--border-primary)}
      #atWorkspace .category-select-modal h3{margin:0 0 20px 0;color:var(--text-primary);font-size:18px}
      #atWorkspace .category-select-list{display:flex;flex-direction:column;gap:8px;max-height:300px;overflow-y:auto;margin-bottom:20px}
      #atWorkspace .category-select-item{padding:12px 16px;background:var(--bg-secondary);border:2px solid var(--border-primary);border-radius:8px;cursor:pointer;transition:all 0.2s;display:flex;align-items:center;gap:10px;color:var(--text-primary)}
      #atWorkspace .category-select-item:hover{background:var(--bg-tertiary);border-color:#2563eb}
      #atWorkspace .category-select-item.selected{background:#eff6ff;border-color:#2563eb}
      [data-theme="dark"] #atWorkspace .category-select-item.selected{background:#1e3a8a}
      
      #atWorkspace .vault-controls{padding:20px 24px;border-bottom:1px solid var(--border-primary);display:flex;gap:16px;flex-wrap:wrap;align-items:center;background:var(--bg-card)}
      #atWorkspace .vault-search{flex:1;min-width:300px;position:relative}
      #atWorkspace .vault-search input{width:100%;padding:12px 40px 12px 16px;border:1px solid var(--border-secondary);border-radius:8px;font-size:0.95rem;background:var(--bg-primary);color:var(--text-primary)}
      #atWorkspace .vault-search input:focus{outline:none;border-color:#2563eb;box-shadow:0 0 0 2px rgba(37,99,235,.1)}
      #atWorkspace .search-clear{position:absolute;right:8px;top:50%;transform:translateY(-50%);background:#dc2626;color:#fff;border:none;width:32px;height:32px;border-radius:6px;cursor:pointer;font-size:18px;display:flex;align-items:center;justify-content:center;transition:all 0.2s}
      #atWorkspace .search-clear:hover{background:#ef4444}
      #atWorkspace .vault-filters{display:flex;gap:10px}
      #atWorkspace .vault-filters select{padding:12px 16px;border:1px solid var(--border-secondary);border-radius:8px;font-size:0.95rem;background:var(--bg-primary);color:var(--text-primary);cursor:pointer}
      #atWorkspace .vault-filters select:focus{outline:none;border-color:#2563eb}
      
      #atWorkspace .vault-stats{padding:20px 24px;background:var(--bg-secondary);display:grid;grid-template-columns:repeat(auto-fit, minmax(150px, 1fr));gap:20px;border-bottom:1px solid var(--border-primary)}
      #atWorkspace .vault-stat{text-align:center}
      #atWorkspace .vault-stat-value{display:block;font-size:1.8rem;font-weight:700;color:var(--text-primary)}
      #atWorkspace .vault-stat-label{display:block;font-size:0.85rem;color:var(--text-secondary);margin-top:4px}
      
      #atWorkspace .vault-content{flex:1;overflow-y:auto;padding:24px;background:var(--bg-tertiary)}
      #atWorkspace .vault-empty{text-align:center;padding:80px 20px;color:var(--text-secondary)}
      #atWorkspace .vault-empty-icon{font-size:4rem;opacity:0.3;margin-bottom:16px}
      
      #atWorkspace .vault-item{background:var(--bg-card);border:1px solid var(--border-primary);border-radius:12px;padding:20px;margin-bottom:16px;display:flex;align-items:center;gap:20px;transition:all 0.2s;cursor:pointer}
      #atWorkspace .vault-item:hover{border-color:#ddd6fe;box-shadow:var(--shadow-md);transform:translateY(-2px)}
      [data-theme="dark"] #atWorkspace .vault-item:hover{border-color:#6366f1}
      #atWorkspace .vault-item-icon{width:56px;height:56px;background:var(--bg-tertiary);border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:28px;flex-shrink:0}
      #atWorkspace .vault-item-info{flex:1;min-width:0}
      #atWorkspace .vault-item-name{font-weight:600;color:var(--text-primary);margin-bottom:6px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:1.05rem}
      #atWorkspace .vault-item-meta{font-size:0.85rem;color:var(--text-secondary);display:flex;gap:20px;flex-wrap:wrap}
      #atWorkspace .vault-item-actions{display:flex;gap:10px;flex-shrink:0}
      
      #atWorkspace .vault-footer{padding:20px 24px;border-top:1px solid var(--border-primary);display:flex;gap:12px;justify-content:space-between;background:var(--bg-card)}
      
      /* File type colors - Enhanced for full size */
      #atWorkspace .vault-item-icon.pdf{background:#fee2e2;color:#dc2626}
      #atWorkspace .vault-item-icon.doc{background:#dbeafe;color:#2563eb}
      #atWorkspace .vault-item-icon.xls{background:#d1fae5;color:#10b981}
      #atWorkspace .vault-item-icon.img{background:#fce7f3;color:#ec4899}
      #atWorkspace .vault-item-icon.html{background:#fef3c7;color:#d97706}
      #atWorkspace .vault-item-icon.other{background:#f3f4f6;color:#6b7280}
      
      /* HTML Display Section */
      #atWorkspace .html-display-section{background:var(--bg-secondary);border-radius:12px;padding:20px;margin-bottom:20px;border:1px solid var(--border-primary)}
      #atWorkspace .html-display-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px}
      #atWorkspace .html-display-header h3{margin:0;color:var(--text-primary);font-size:1.2rem}
      #atWorkspace .html-paste-btn{background:#2563eb;color:#fff;border:none;padding:8px 16px;border-radius:6px;cursor:pointer;font-size:0.9rem;transition:all 0.2s}
      #atWorkspace .html-paste-btn:hover{background:#1d4ed8;transform:translateY(-1px)}
      
      #atWorkspace .html-items-container{display:flex;flex-direction:column;gap:12px}
      #atWorkspace .html-item{background:var(--bg-card);border:1px solid var(--border-primary);border-radius:8px;padding:16px;position:relative;transition:all 0.2s}
      #atWorkspace .html-item:hover{border-color:#ddd6fe;box-shadow:var(--shadow-sm)}
      [data-theme="dark"] #atWorkspace .html-item:hover{border-color:#6366f1}
      #atWorkspace .html-item-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
      #atWorkspace .html-item-title{font-weight:600;color:var(--text-primary);font-size:1rem}
      #atWorkspace .html-item-controls{display:flex;gap:8px}
      #atWorkspace .html-control-btn{background:var(--bg-tertiary);border:none;padding:6px 10px;border-radius:4px;cursor:pointer;font-size:0.8rem;transition:all 0.2s;color:var(--text-primary)}
      #atWorkspace .html-control-btn:hover{background:var(--border-primary)}
      #atWorkspace .html-control-btn.move-up{color:#2563eb}
      #atWorkspace .html-control-btn.move-down{color:#2563eb}
      #atWorkspace .html-control-btn.delete{color:#dc2626}
      #atWorkspace .html-control-btn.fullscreen{color:#10b981}
      #atWorkspace .html-control-btn:disabled{opacity:0.5;cursor:not-allowed}
      
      #atWorkspace .html-content-frame{width:100%;min-height:300px;border:1px solid var(--border-primary);border-radius:6px;background:var(--bg-card)}
      #atWorkspace .html-empty-state{text-align:center;padding:60px 20px;color:var(--text-secondary)}
      #atWorkspace .html-empty-icon{font-size:3rem;opacity:0.3;margin-bottom:12px}
      
      /* Fullscreen HTML Display */
      #atWorkspace .html-fullscreen-overlay{position:fixed;inset:0;background:var(--bg-primary);z-index:2000;display:none}
      #atWorkspace .html-fullscreen-overlay.show{display:flex;flex-direction:column}
      #atWorkspace .html-fullscreen-header{background:#1f2937;color:#fff;padding:12px 20px;display:flex;justify-content:space-between;align-items:center;box-shadow:0 2px 8px rgba(0,0,0,0.1)}
      [data-theme="dark"] #atWorkspace .html-fullscreen-header{background:#0f172a}
      #atWorkspace .html-fullscreen-title{font-size:1.1rem;font-weight:600}
      #atWorkspace .html-fullscreen-controls{display:flex;gap:12px}
      #atWorkspace .html-fullscreen-btn{background:rgba(255,255,255,0.1);border:none;color:#fff;padding:8px 16px;border-radius:6px;cursor:pointer;transition:all 0.2s;font-size:0.9rem}
      #atWorkspace .html-fullscreen-btn:hover{background:rgba(255,255,255,0.2)}
      #atWorkspace .html-fullscreen-content{flex:1;position:relative;overflow:hidden}
      #atWorkspace .html-fullscreen-iframe{width:100%;height:100%;border:none;background:var(--bg-card)}
      
      /* HTML Paste Modal */
      #atWorkspace .html-paste-modal{background:var(--bg-card);border-radius:12px;width:90%;max-width:700px;padding:24px;border:1px solid var(--border-primary)}
      #atWorkspace .html-paste-modal h3{margin:0 0 16px 0;color:var(--text-primary)}
      #atWorkspace .html-paste-modal textarea{width:100%;min-height:300px;padding:12px;border:2px solid var(--border-primary);border-radius:8px;font-family:monospace;font-size:14px;resize:vertical;background:var(--bg-primary);color:var(--text-primary)}
      #atWorkspace .html-paste-modal input{width:100%;padding:10px 12px;border:2px solid var(--border-primary);border-radius:6px;margin-bottom:12px;background:var(--bg-primary);color:var(--text-primary)}
      @media (max-width: 768px) {
          #atWorkspace .grid{grid-template-columns:1fr}
          #atWorkspace .vault-modal{width:100%;height:100vh;max-height:100vh;border-radius:0}
          #atWorkspace .vault-header{border-radius:0}
          #atWorkspace .vault-controls{flex-direction:column;align-items:stretch}
          #atWorkspace .vault-search{min-width:auto}
          #atWorkspace .vault-filters{flex-direction:column;width:100%}
          #atWorkspace .vault-filters select{width:100%}
          #atWorkspace .vault-item{flex-wrap:wrap}
          #atWorkspace .vault-item-info{width:100%}
          #atWorkspace .vault-item-actions{width:100%;margin-top:12px;justify-content:stretch}
          #atWorkspace .vault-item-actions .pill{flex:1;text-align:center}
          #atWorkspace .vault-footer{flex-direction:column}
          #atWorkspace .vault-footer button{width:100%}
      }
    </style>
</head>
<body>
    <div id="atWorkspaceWrapper">
        <!-- Theme Toggle Button -->
        <button class="theme-toggle-global" onclick="App.toggleGlobalTheme()" title="Toggle dark mode">
            <span class="icon" id="themeIcon">🌙</span>
        </button>

        <!-- Sync Status Indicator -->
        <div class="sync-status" id="syncStatus">
            <span class="sync-dot"></span>
            <span id="syncText">Local Mode</span>
        </div>

        <div id="atWorkspace">
            <header>
                <div>
                    <h1>🚌 AT-AC Transition Programme</h1>
                    <div class="subtitle">Collaborative Workspace & Document Hub</div>
                </div>
                <button class="btn vault-btn" id="openVaultTop" onclick="App.openVault()">
                    📂 Document Vault
                    <span class="vault-badge" id="vaultBadge">0</span>
                </button>
            </header>
            
            <!-- Quick Stats -->
            <div class="stats-bar" id="statsBar">
                <div class="stat-item">
                    <div class="stat-value" id="totalItems">0</div>
                    <div class="stat-label">Total Items</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="activeWorkstreams">0</div>
                    <div class="stat-label">Active Workstreams</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="upcomingMilestones">0</div>
                    <div class="stat-label">Upcoming Milestones</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="totalDocuments">0</div>
                    <div class="stat-label">Documents</div>
                </div>
            </div>
            
            <nav>
                <div class="tab" data-type="overview">📊 Programme Overview</div>
                <div class="tab" data-type="workstreams">🔄 Workstreams</div>
                <div class="tab" data-type="milestones">🎯 Milestones</div>
                <div class="tab" data-type="resources">📚 Resources</div>
            </nav>
            
            <main></main>

            <!-- Item Modal -->
            <div class="overlay" id="modalOv">
                <div class="modal">
                    <h3 id="modalHead">New Item</h3>
                    <input id="titleInput" placeholder="Title" required>
                    <textarea id="descInput" placeholder="Description" rows="3"></textarea>
                    
                    <!-- Priority selector -->
                    <div>
                        <label style="font-size:.9rem;margin-bottom:6px;display:block">Priority Level</label>
                        <div class="priority-selector">
                            <div class="priority-option" data-priority="high">🔴 High</div>
                            <div class="priority-option selected" data-priority="medium">🟡 Medium</div>
                            <div class="priority-option" data-priority="low">🟢 Low</div>
                        </div>
                    </div>
                    
                    <!-- Organization tags -->
                    <div>
                        <label style="font-size:.9rem;margin-bottom:6px;display:block">Organization</label>
                        <select id="orgSelect">
                            <option value="">Select organization...</option>
                            <option value="at">Auckland Transport</option>
                            <option value="ac">Auckland Council</option>
                            <option value="integrated">Integrated/Joint</option>
                        </select>
                    </div>
                    
                    <!-- Resource Type for Resources section -->
                    <div id="resourceTypeGroup" style="display:none">
                        <label style="font-size:.9rem;margin-bottom:6px;display:block">Resource Type</label>
                        <select id="resourceTypeSelect">
                            <option value="document">Document</option>
                            <option value="link">Web Link</option>
                            <option value="drive">Google Drive</option>
                        </select>
                    </div>
                    
                    <!-- Resource URL for Resources section -->
                    <div id="resourceUrlGroup" style="display:none">
                        <label style="font-size:.9rem;margin-bottom:6px;display:block">Resource URL</label>
                        <input type="url" id="resourceUrlInput" placeholder="Enter the URL to open when card is clicked">
                    </div>
                    
                    <!-- Due date for milestones -->
                    <div id="dueDateGroup" style="display:none">
                        <label style="font-size:.9rem;margin-bottom:6px;display:block">Due Date</label>
                        <input type="date" id="dueDateInput">
                    </div>
                    
                    <div class="link-input-group" style="display:flex;gap:6px">
                        <input id="linkInput" placeholder="Add URL" style="flex:1">
                        <button class="btn" id="addLink">＋</button>
                    </div>
                    <div id="linkPreview" class="link-preview" style="font-size:.75rem;color:#6b7280"></div>
                    
                    <input id="driveInput" placeholder="Google Drive folder URL (optional)">
                    
                    <div>
                        <label style="font-size:.9rem;margin-bottom:6px;display:block">📎 Upload Documents</label>
                        <input type="file" id="fileInput" multiple accept=".pdf,.doc,.docx,.txt,.xlsx,.pptx,.jpg,.png,.html,.htm">
                        <div id="filePreview" class="file-upload-preview"></div>
                    </div>
                    
                    <div style="display:flex;gap:8px;justify-content:flex-end">
                        <button class="btn" id="cancelBtn">Cancel</button>
                        <button class="btn" style="background:#2563eb;color:#fff" id="saveBtn">Save</button>
                    </div>
                </div>
            </div>

            <!-- Notification -->
            <div class="notification" id="notification"></div>
            
            <!-- Vault Modal -->
            <div class="overlay" id="vaultOverlay" data-testid="vault-overlay">
                <div class="vault-modal">
                    <div class="vault-header">
                        <h2>📂 Document Vault</h2>
                        <button class="vault-close" onclick="App.closeVault()">×</button>
                    </div>
                    
                    <!-- Category Management Bar -->
                    <div class="category-bar">
                        <div class="category-tabs" id="categoryTabs">
                            <!-- Categories will be rendered here -->
                        </div>
                        <button class="add-category-btn" onclick="App.showCategoryModal()">
                            <span>+</span> Add Category
                        </button>
                    </div>
                    
                    <div class="vault-controls">
                        <div class="vault-search">
                            <input type="text" id="vaultSearch" placeholder="Search documents..." onkeyup="App.searchVault()">
                            <button class="search-clear" id="searchClear" onclick="App.clearSearch()" style="display:none">×</button>
                        </div>
                        <div class="vault-filters">
                            <select id="vaultFilter" onchange="App.filterVault()">
                                <option value="all">All Documents</option>
                                <option value="pdf">PDF Files</option>
                                <option value="doc">Word Documents</option>
                                <option value="xls">Spreadsheets</option>
                                <option value="img">Images</option>
                                <option value="html">HTML Files</option>
                                <option value="other">Other</option>
                            </select>
                            <select id="vaultSort" onchange="App.sortVault()">
                                <option value="date-desc">Newest First</option>
                                <option value="date-asc">Oldest First</option>
                                <option value="name-asc">Name (A-Z)</option>
                                <option value="name-desc">Name (Z-A)</option>
                                <option value="size-desc">Largest First</option>
                                <option value="size-asc">Smallest First</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="vault-stats">
                        <div class="vault-stat">
                            <span class="vault-stat-value" id="vaultTotal">0</span>
                            <span class="vault-stat-label">Total Files</span>
                        </div>
                        <div class="vault-stat">
                            <span class="vault-stat-value" id="vaultSize">0 MB</span>
                            <span class="vault-stat-label">Total Size</span>
                        </div>
                        <div class="vault-stat">
                            <span class="vault-stat-value" id="vaultRecent">0</span>
                            <span class="vault-stat-label">Added This Week</span>
                        </div>
                        <div class="vault-stat">
                            <span class="vault-stat-value" id="categoryCount">0</span>
                            <span class="vault-stat-label">In Category</span>
                        </div>
                    </div>
                    
                    <div class="vault-content" id="vaultContent">
                        <div class="vault-empty">
                            <div class="vault-empty-icon">⏳</div>
                            <p>Loading vault...</p>
                        </div>
                    </div>
                    
                    <div class="vault-footer">
                        <button class="btn" style="background:#6b7280;color:#fff" onclick="App.exportVaultList()">📥 Export List</button>
                        <button class="btn" style="background:#dc2626;color:#fff" onclick="App.clearVault()" id="clearVaultBtn">🗑️ Clear Vault</button>
                    </div>
                </div>
            </div>
            
            <!-- Category Modal -->
            <div class="overlay" id="categoryModalOverlay">
                <div class="category-modal">
                    <h3 id="categoryModalTitle">Add New Category</h3>
                    <form class="modal-form" id="categoryForm" onsubmit="App.saveCategory(event)">
                        <div>
                            <label for="categoryName">Category Name</label>
                            <input type="text" id="categoryName" required placeholder="Enter category name">
                        </div>
                        <div>
                            <label>Category Color</label>
                            <div class="color-picker" id="colorPicker">
                                <div class="color-option" data-color="#FF6B6B" style="background: #FF6B6B"></div>
                                <div class="color-option" data-color="#4ECDC4" style="background: #4ECDC4"></div>
                                <div class="color-option" data-color="#45B7D1" style="background: #45B7D1"></div>
                                <div class="color-option" data-color="#FFA07A" style="background: #FFA07A"></div>
                                <div class="color-option" data-color="#98D8C8" style="background: #98D8C8"></div>
                                <div class="color-option" data-color="#FDCB6E" style="background: #FDCB6E"></div>
                                <div class="color-option" data-color="#6C5CE7" style="background: #6C5CE7"></div>
                                <div class="color-option" data-color="#A8E6CF" style="background: #A8E6CF"></div>
                                <div class="color-option" data-color="#FFD93D" style="background: #FFD93D"></div>
                                <div class="color-option selected" data-color="#0066CC" style="background: #0066CC"></div>
                            </div>
                        </div>
                        <div class="modal-actions">
                            <button type="button" class="modal-btn secondary" onclick="App.closeCategoryModal()">Cancel</button>
                            <button type="submit" class="modal-btn primary">Save</button>
                        </div>
                    </form>
                </div>
            </div>
            
            <!-- Edit Category Modal -->
            <div class="overlay" id="editCategoryOverlay">
                <div class="category-modal">
                    <h3>Edit Category</h3>
                    <form class="modal-form" id="editCategoryForm" onsubmit="App.updateCategory(event)">
                        <div>
                            <label for="editCategoryName">Category Name</label>
                            <input type="text" id="editCategoryName" required placeholder="Enter category name">
                        </div>
                        <div>
                            <label>Category Color</label>
                            <div class="color-picker" id="editColorPicker">
                                <div class="color-option" data-color="#FF6B6B" style="background: #FF6B6B"></div>
                                <div class="color-option" data-color="#4ECDC4" style="background: #4ECDC4"></div>
                                <div class="color-option" data-color="#45B7D1" style="background: #45B7D1"></div>
                                <div class="color-option" data-color="#FFA07A" style="background: #FFA07A"></div>
                                <div class="color-option" data-color="#98D8C8" style="background: #98D8C8"></div>
                                <div class="color-option" data-color="#FDCB6E" style="background: #FDCB6E"></div>
                                <div class="color-option" data-color="#6C5CE7" style="background: #6C5CE7"></div>
                                <div class="color-option" data-color="#A8E6CF" style="background: #A8E6CF"></div>
                                <div class="color-option" data-color="#FFD93D" style="background: #FFD93D"></div>
                                <div class="color-option" data-color="#0066CC" style="background: #0066CC"></div>
                            </div>
                        </div>
                        <div class="modal-actions">
                            <button type="button" class="modal-btn secondary" onclick="App.closeEditCategoryModal()">Cancel</button>
                            <button type="submit" class="modal-btn primary">Update</button>
                        </div>
                    </form>
                </div>
            </div>
            
            <!-- Document Preview Modal -->
            <div class="overlay" id="previewOverlay">
                <div class="preview-modal">
                    <div class="preview-header">
                        <h3 id="previewTitle">Document Preview</h3>
                        <button class="vault-close" onclick="App.closePreview()" style="background:rgba(255,255,255,0.1)">×</button>
                    </div>
                    <div class="preview-content" id="previewContent">
                        <!-- Preview content will be loaded here -->
                    </div>
                </div>
            </div>
            
            <!-- Category Selection Modal -->
            <div class="overlay" id="categorySelectOverlay">
                <div class="category-select-modal">
                    <h3>Select Category for Document</h3>
                    <div class="category-select-list" id="categorySelectList">
                        <!-- Categories will be rendered here -->
                    </div>
                    <div class="modal-actions">
                        <button type="button" class="modal-btn secondary" onclick="App.closeCategorySelect()">Cancel</button>
                        <button type="button" class="modal-btn primary" onclick="App.confirmCategorySelect()">Add to Vault</button>
                    </div>
                </div>
            </div>
            
            <!-- HTML Paste Modal -->
            <div class="overlay" id="htmlPasteOverlay">
                <div class="html-paste-modal">
                    <h3>Add HTML Content</h3>
                    <form id="htmlPasteForm" onsubmit="App.saveHtmlContent(event)">
                        <div>
                            <label style="font-size:0.9rem;color:#6b7280;margin-bottom:6px;display:block">Title</label>
                            <input type="text" id="htmlTitle" placeholder="Enter a title for this content" required>
                        </div>
                        <div>
                            <label style="font-size:0.9rem;color:#6b7280;margin-bottom:6px;display:block">HTML Content</label>
                            <textarea id="htmlContent" placeholder="Paste your HTML content here..." required></textarea>
                        </div>
                        <div class="modal-actions">
                            <button type="button" class="modal-btn secondary" onclick="App.closeHtmlPasteModal()">Cancel</button>
                            <button type="submit" class="modal-btn primary">Add Content</button>
                        </div>
                    </form>
                </div>
            </div>
            
            <!-- HTML Fullscreen Display -->
            <div class="html-fullscreen-overlay" id="htmlFullscreenOverlay">
                <div class="html-fullscreen-header">
                    <div class="html-fullscreen-title" id="fullscreenTitle">HTML Content</div>
                    <div class="html-fullscreen-controls">
                        <button class="html-fullscreen-btn" onclick="App.toggleFullscreenMode()">🔄 Toggle Fullscreen</button>
                        <button class="html-fullscreen-btn" onclick="App.closeHtmlFullscreen()">✕ Close</button>
                    </div>
                </div>
                <div class="html-fullscreen-content">
                    <iframe class="html-fullscreen-iframe" id="fullscreenIframe"></iframe>
                </div>
            </div>
        </div>
    </div>

    <script>
    // AT-AC Workspace Script
    const App = {
        // State
        state: {
            view: 'overview',
            cards: {
                overview: {},
                workstreams: {},
                milestones: {},
                resources: {}
            },
            vault: [],
            vaultCategories: [
                { id: 'general', name: 'General', color: '#0066CC' }
            ],
            currentCategory: 'general',
            themes: {},
            nextId: 1,
            editingId: null,
            editingType: null,
            selectedPriority: 'medium',
            currentVaultFilter: 'all',
            currentVaultSort: 'date-desc',
            vaultSearchTerm: '',
            pendingVaultFile: null, // For category selection
            editingCategoryId: null, // For editing categories
            htmlDisplayItems: [], // For HTML display on overview
            globalTheme: 'light' // Global theme preference
        },

        // Initialize
        init() {
            this.loadData();
            this.applyTheme();
            this.setupEventListeners();
            this.renderPanels();
            this.renderCards();
            this.updateStats();
            
            // Set initial tab
            const tab = document.querySelector('.tab[data-type="' + this.state.view + '"]');
            if (tab) tab.click();
            
            // Always render HTML items after panels are created
            setTimeout(() => {
                this.renderHtmlItems();
            }, 100);
        },

        // Apply theme
        applyTheme() {
            const theme = this.state.globalTheme || 'light';
            document.documentElement.setAttribute('data-theme', theme);
            document.getElementById('themeIcon').textContent = theme === 'dark' ? '☀️' : '🌙';
        },

        // Toggle global theme
        toggleGlobalTheme() {
            this.state.globalTheme = this.state.globalTheme === 'dark' ? 'light' : 'dark';
            this.applyTheme();
            this.saveData();
            this.showNotification(`Switched to ${this.state.globalTheme} mode`);
        },

        // Load data from localStorage
        loadData() {
            try {
                const saved = localStorage.getItem('atWorkspaceStore');
                if (saved) {
                    const data = JSON.parse(saved);
                    // Merge loaded data with defaults, preserving any missing properties
                    this.state = { 
                        ...this.state, 
                        ...data,
                        // Ensure htmlDisplayItems is an array
                        htmlDisplayItems: data.htmlDisplayItems || []
                    };
                    console.log('Loaded state:', this.state);
                }
            } catch (e) {
                console.error('Failed to load data:', e);
            }
        },

        // Save data to localStorage
        saveData() {
            try {
                localStorage.setItem('atWorkspaceStore', JSON.stringify(this.state));
            } catch (e) {
                console.error('Failed to save data:', e);
            }
        },

        // Setup event listeners
        setupEventListeners() {
            // Tab switching
            document.querySelectorAll('.tab').forEach(tab => {
                tab.addEventListener('click', () => this.switchTab(tab.dataset.type));
            });

            // Modal buttons
            document.getElementById('saveBtn').addEventListener('click', () => this.saveItem());
            document.getElementById('cancelBtn').addEventListener('click', () => this.closeModal());

            // Priority options
            document.querySelectorAll('.priority-option').forEach(opt => {
                opt.addEventListener('click', () => this.selectPriority(opt));
            });

            // Links
            document.getElementById('addLink').addEventListener('click', () => this.addLink());
            document.getElementById('linkPreview').addEventListener('click', (e) => {
                if (e.target.dataset.rm !== undefined) {
                    this.removeLink(parseInt(e.target.dataset.rm));
                }
            });

            // Files
            document.getElementById('fileInput').addEventListener('change', (e) => this.handleFileSelect(e));
            document.getElementById('filePreview').addEventListener('click', (e) => {
                if (e.target.dataset.rmfile !== undefined) {
                    this.removeFile(parseInt(e.target.dataset.rmfile));
                }
            });

            // Close modals on overlay click
            document.getElementById('modalOv').addEventListener('click', (e) => {
                if (e.target.id === 'modalOv') this.closeModal();
            });
            document.getElementById('vaultOverlay').addEventListener('click', (e) => {
                if (e.target.id === 'vaultOverlay') this.closeVault();
            });
            document.getElementById('categoryModalOverlay').addEventListener('click', (e) => {
                if (e.target.id === 'categoryModalOverlay') this.closeCategoryModal();
            });
            document.getElementById('previewOverlay').addEventListener('click', (e) => {
                if (e.target.id === 'previewOverlay') this.closePreview();
            });
            document.getElementById('categorySelectOverlay').addEventListener('click', (e) => {
                if (e.target.id === 'categorySelectOverlay') this.closeCategorySelect();
            });
            document.getElementById('editCategoryOverlay').addEventListener('click', (e) => {
                if (e.target.id === 'editCategoryOverlay') this.closeEditCategoryModal();
            });
            document.getElementById('htmlPasteOverlay').addEventListener('click', (e) => {
                if (e.target.id === 'htmlPasteOverlay') this.closeHtmlPasteModal();
            });

            // Color picker for both modals
            document.querySelectorAll('#colorPicker .color-option, #editColorPicker .color-option').forEach(opt => {
                opt.addEventListener('click', (e) => {
                    const picker = e.target.closest('.color-picker');
                    picker.querySelectorAll('.color-option').forEach(o => o.classList.remove('selected'));
                    e.target.classList.add('selected');
                });
            });

            // Close category menu when clicking outside
            document.addEventListener('click', (e) => {
                if (!e.target.closest('.category-menu-btn') && !e.target.closest('.category-menu')) {
                    document.querySelectorAll('.category-menu').forEach(menu => menu.classList.remove('show'));
                }
            });

            // Keyboard shortcuts
            document.addEventListener('keydown', (e) => {
                if (e.key === 'Escape') {
                    // Check if fullscreen HTML is open first
                    if (document.getElementById('htmlFullscreenOverlay').classList.contains('show')) {
                        this.closeHtmlFullscreen();
                    } else {
                        this.closeModal();
                        this.closeVault();
                        this.closeCategoryModal();
                        this.closePreview();
                        this.closeCategorySelect();
                        this.closeEditCategoryModal();
                        this.closeHtmlPasteModal();
                    }
                }
                if ((e.ctrlKey || e.metaKey) && e.key === 'k') {
                    e.preventDefault();
                    this.openVault();
                }
            });
        },

        // Render panels
        renderPanels() {
            const main = document.querySelector('main');
            const types = ['overview', 'workstreams', 'milestones', 'resources'];
            const titles = {
                overview: 'Programme Overview',
                workstreams: 'Active Workstreams',
                milestones: 'Key Milestones',
                resources: 'Resources & Documents'
            };

            types.forEach(type => {
                const panel = document.createElement('section');
                panel.id = type;
                panel.className = 'panel';
                
                if (type === 'overview') {
                    // Special layout for overview with HTML display section
                    panel.innerHTML = `
                        <div class="panel-header">
                            <h2>${titles[type]}</h2>
                            <button class="add-btn" onclick="App.openModal('${type}')">+ Add ${type.slice(0, -1)}</button>
                        </div>
                        
                        <!-- HTML Display Section -->
                        <div class="html-display-section">
                            <div class="html-display-header">
                                <h3>📄 HTML Content Display</h3>
                                <button class="html-paste-btn" onclick="App.openHtmlPasteModal()">+ Add HTML</button>
                            </div>
                            <div class="html-items-container" id="htmlItemsContainer">
                                <!-- HTML items will be rendered here -->
                            </div>
                        </div>
                        
                        <div class="grid" id="grid_${type}"></div>
                    `;
                } else {
                    panel.innerHTML = `
                        <div class="panel-header">
                            <h2>${titles[type]}</h2>
                            <button class="add-btn" onclick="App.openModal('${type}')">+ Add ${type.slice(0, -1)}</button>
                        </div>
                        <div class="grid" id="grid_${type}"></div>
                    `;
                }
                main.appendChild(panel);
            });
        },

        // Switch tab
        switchTab(type) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelector(`.tab[data-type="${type}"]`).classList.add('active');
            
            document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
            document.getElementById(type).classList.add('active');
            
            this.state.view = type;
            this.saveData();
            
            // Always render HTML items when switching to overview
            if (type === 'overview') {
                setTimeout(() => {
                    this.renderHtmlItems();
                }, 50);
            }
        },

        // Modal state
        linksTemp: [],
        filesTemp: [],

        // Open modal
        openModal(type, id = null) {
            this.state.editingType = type;
            this.state.editingId = id;
            
            const modal = document.getElementById('modalOv');
            const title = document.getElementById('titleInput');
            const desc = document.getElementById('descInput');
            const org = document.getElementById('orgSelect');
            const dueDate = document.getElementById('dueDateInput');
            const drive = document.getElementById('driveInput');
            const linkInput = document.getElementById('linkInput');
            const resourceType = document.getElementById('resourceTypeSelect');
            const resourceUrl = document.getElementById('resourceUrlInput');
            
            if (id && this.state.cards[type][id]) {
                const card = this.state.cards[type][id];
                document.getElementById('modalHead').textContent = 'Edit ' + type.slice(0, -1);
                title.value = card.title || '';
                desc.value = card.desc || '';
                org.value = card.org || '';
                dueDate.value = card.dueDate || '';
                drive.value = card.drive || '';
                resourceType.value = card.resourceType || 'document';
                resourceUrl.value = card.resourceUrl || '';
                this.state.selectedPriority = card.priority || 'medium';
                this.linksTemp = [...(card.links || [])];
                this.filesTemp = [];
            } else {
                document.getElementById('modalHead').textContent = 'New ' + type.slice(0, -1);
                title.value = '';
                desc.value = '';
                org.value = '';
                dueDate.value = '';
                drive.value = '';
                linkInput.value = '';
                resourceType.value = 'document';
                resourceUrl.value = '';
                this.state.selectedPriority = 'medium';
                this.linksTemp = [];
                this.filesTemp = [];
            }
            
            // Show/hide fields based on type
            document.getElementById('dueDateGroup').style.display = type === 'milestones' ? 'block' : 'none';
            document.getElementById('resourceTypeGroup').style.display = type === 'resources' ? 'block' : 'none';
            document.getElementById('resourceUrlGroup').style.display = type === 'resources' ? 'block' : 'none';
            
            // Update priority selection
            document.querySelectorAll('.priority-option').forEach(opt => {
                opt.classList.toggle('selected', opt.dataset.priority === this.state.selectedPriority);
            });
            
            // Reset file input
            document.getElementById('fileInput').value = '';
            
            this.renderLinks();
            this.renderFiles();
            modal.classList.add('show');
            title.focus();
        },

        // Close modal
        closeModal() {
            const modal = document.getElementById('modalOv');
            modal.classList.remove('show');
            modal.style.display = 'none';
            setTimeout(() => {
                modal.style.display = '';
            }, 10);
            this.state.editingType = null;
            this.state.editingId = null;
        },

        // Select priority
        selectPriority(option) {
            document.querySelectorAll('.priority-option').forEach(opt => opt.classList.remove('selected'));
            option.classList.add('selected');
            this.state.selectedPriority = option.dataset.priority;
        },

        // Add link
        addLink() {
            const input = document.getElementById('linkInput');
            const url = input.value.trim();
            if (!url) return;
            
            try {
                new URL(url);
                this.linksTemp.push(url);
                input.value = '';
                this.renderLinks();
            } catch {
                alert('Invalid URL');
            }
        },

        // Remove link
        removeLink(index) {
            this.linksTemp.splice(index, 1);
            this.renderLinks();
        },

        // Render links
        renderLinks() {
            const preview = document.getElementById('linkPreview');
            preview.innerHTML = this.linksTemp.length ? 
                this.linksTemp.map((l, i) => `
                    <span style="display:block;margin:2px 0">
                        ${l} <b data-rm='${i}' style='cursor:pointer;color:#dc2626;margin-left:8px'>×</b>
                    </span>
                `).join('') :
                '<em style="color:#9ca3af">No links yet</em>';
        },

        // Handle file select
        handleFileSelect(e) {
            this.filesTemp = [...e.target.files];
            
            // Read file contents for preview
            this.filesTemp.forEach((file, index) => {
                const reader = new FileReader();
                
                if (file.type === 'text/html' || file.name.endsWith('.html') || file.name.endsWith('.htm') || 
                    file.type.startsWith('text/') || file.name.endsWith('.txt')) {
                    // Read text content
                    reader.onload = (event) => {
                        this.filesTemp[index].content = event.target.result;
                    };
                    reader.readAsText(file);
                } else {
                    // Read as base64 for all other files
                    reader.onload = (event) => {
                        this.filesTemp[index].dataUrl = event.target.result;
                        this.filesTemp[index].base64 = event.target.result.split(',')[1];
                    };
                    reader.readAsDataURL(file);
                }
            });
            
            this.renderFiles();
        },

        // Remove file
        removeFile(index) {
            this.filesTemp.splice(index, 1);
            this.renderFiles();
        },

        // Render files
        renderFiles() {
            const preview = document.getElementById('filePreview');
            preview.innerHTML = this.filesTemp.length ?
                '<div>' + this.filesTemp.map((f, i) => 
                    `<div class="file-upload-item">
                        <span>📎 ${f.name} (${(f.size / 1024).toFixed(1)} KB)</span>
                        <b data-rmfile='${i}' style='cursor:pointer;color:#dc2626'>×</b>
                    </div>`
                ).join('') + '</div>' :
                '<em style="color:#9ca3af">No files selected</em>';
        },

        // Save item
        saveItem() {
            const title = document.getElementById('titleInput').value.trim();
            if (!title) {
                alert('Title is required');
                return;
            }

            const type = this.state.editingType;
            const id = this.state.editingId || this.state.nextId++;
            
            const existingCard = this.state.editingId ? this.state.cards[type][id] : null;
            const existingFiles = existingCard ? existingCard.files || [] : [];

            const newFiles = this.filesTemp.map(f => ({
                id: 'file_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9),
                name: f.name,
                size: f.size,
                type: f.type,
                uploadDate: new Date().toISOString(),
                inVault: false,
                content: f.content || null,
                dataUrl: f.dataUrl || null,
                base64: f.base64 || null
            }));

            const allFiles = [...existingFiles, ...newFiles];

            this.state.cards[type][id] = {
                id,
                title,
                desc: document.getElementById('descInput').value.trim(),
                org: document.getElementById('orgSelect').value,
                priority: this.state.selectedPriority,
                dueDate: document.getElementById('dueDateInput').value,
                drive: document.getElementById('driveInput').value.trim(),
                resourceType: type === 'resources' ? document.getElementById('resourceTypeSelect').value : null,
                resourceUrl: type === 'resources' ? document.getElementById('resourceUrlInput').value.trim() : null,
                links: [...this.linksTemp],
                files: allFiles,
                created: existingCard ? existingCard.created : new Date().toISOString(),
                updated: new Date().toISOString(),
                completed: existingCard ? existingCard.completed : false
            };

            this.saveData();
            this.renderCards();
            this.updateStats();
            this.closeModal();
            
            if (newFiles.length > 0) {
                this.showNotification(`Added ${newFiles.length} file(s) to ${title}`);
            }
        },

        // Delete card
        deleteCard(type, id) {
            if (confirm('Delete this item?')) {
                delete this.state.cards[type][id];
                delete this.state.themes[`${type}_${id}`];
                this.saveData();
                this.renderCards();
                this.updateStats();
                this.showNotification('Item deleted');
            }
        },

        // Toggle theme
        toggleCardTheme(type, id) {
            const key = `${type}_${id}`;
            this.state.themes[key] = this.state.themes[key] === 'dark' ? 'light' : 'dark';
            this.saveData();
            this.renderCards();
        },

        // Open resource
        openResource(type, id) {
            const card = this.state.cards[type][id];
            if (!card || type !== 'resources') return;
            
            if (card.resourceUrl) {
                // Open URL in new tab
                window.open(card.resourceUrl, '_blank');
                this.showNotification(`Opening ${card.title}...`);
            } else if (card.drive) {
                // Open Google Drive folder
                window.open(card.drive, '_blank');
                this.showNotification(`Opening Drive folder...`);
            } else if (card.links && card.links.length > 0) {
                // Open first link
                window.open(card.links[0], '_blank');
                this.showNotification(`Opening ${card.title}...`);
            } else {
                this.showNotification('No URL configured for this resource', 'error');
            }
        },

        // Toggle completion
        toggleComplete(type, id) {
            const card = this.state.cards[type][id];
            if (!card) return;
            
            card.completed = !card.completed;
            this.saveData();
            this.updateStats();
            this.renderCards();
        },

        // Move file to vault
        moveFileToVault(type, id, fileId) {
            const card = this.state.cards[type][id];
            if (!card) return;
            
            const fileIndex = card.files.findIndex(f => f.id === fileId);
            if (fileIndex === -1) return;
            
            const file = card.files[fileIndex];
            
            if (file.inVault) {
                this.showNotification(`"${file.name}" is already in the vault`);
                return;
            }
            
            // Store pending file info and show category selection
            this.state.pendingVaultFile = {
                type: type,
                cardId: id,
                fileId: fileId,
                file: file,
                cardTitle: card.title
            };
            
            this.showCategorySelect();
        },

        // Show category selection modal
        showCategorySelect() {
            const modal = document.getElementById('categorySelectOverlay');
            const list = document.getElementById('categorySelectList');
            
            // Render categories
            list.innerHTML = this.state.vaultCategories.map(cat => `
                <div class="category-select-item" data-category-id="${cat.id}" onclick="App.selectVaultCategory('${cat.id}')">
                    <span class="category-color" style="background: ${cat.color}; width: 16px; height: 16px; border-radius: 50%;"></span>
                    <span>${cat.name}</span>
                </div>
            `).join('');
            
            // Select first category by default
            if (this.state.vaultCategories.length > 0) {
                this.selectVaultCategory(this.state.vaultCategories[0].id);
            }
            
            modal.classList.add('show');
        },

        // Select category for vault
        selectVaultCategory(categoryId) {
            document.querySelectorAll('.category-select-item').forEach(item => {
                item.classList.toggle('selected', item.dataset.categoryId === categoryId);
            });
            this.state.selectedVaultCategory = categoryId;
        },

        // Close category select modal
        closeCategorySelect() {
            document.getElementById('categorySelectOverlay').classList.remove('show');
            this.state.pendingVaultFile = null;
            this.state.selectedVaultCategory = null;
        },

        // Confirm category selection and add to vault
        confirmCategorySelect() {
            if (!this.state.pendingVaultFile || !this.state.selectedVaultCategory) return;
            
            const { type, cardId, fileId, file, cardTitle } = this.state.pendingVaultFile;
            const category = this.state.selectedVaultCategory;
            
            // Add to vault
            this.state.vault.push({
                id: fileId,
                name: file.name,
                size: file.size,
                type: file.type,
                date: new Date().toISOString(),
                source: `${type}: ${cardTitle}`,
                category: category,
                content: file.content || null,
                dataUrl: file.dataUrl || null,
                base64: file.base64 || null
            });
            
            // Mark file as in vault
            const card = this.state.cards[type][cardId];
            if (card) {
                const fileIndex = card.files.findIndex(f => f.id === fileId);
                if (fileIndex !== -1) {
                    card.files[fileIndex].inVault = true;
                }
            }
            
            this.saveData();
            this.renderCards();
            this.updateStats();
            this.closeCategorySelect();
            
            const categoryName = this.getCategoryName(category);
            this.showNotification(`✅ "${file.name}" added to vault in ${categoryName}`);
        },

        // Remove file from card
        removeFileFromCard(type, id, fileId) {
            const card = this.state.cards[type][id];
            if (!card) return;
            
            const fileIndex = card.files.findIndex(f => f.id === fileId);
            if (fileIndex === -1) return;
            
            const file = card.files[fileIndex];
            
            if (confirm(`Remove "${file.name}" from this item?`)) {
                card.files.splice(fileIndex, 1);
                this.saveData();
                this.renderCards();
                this.updateStats();
            }
        },

        // Render cards
        renderCards() {
            ['overview', 'workstreams', 'milestones', 'resources'].forEach(type => {
                const grid = document.getElementById('grid_' + type);
                const cards = Object.values(this.state.cards[type] || {});
                
                if (cards.length === 0) {
                    grid.innerHTML = '<p style="text-align:center;color:#6b7280;grid-column:1/-1;padding:40px">No items yet. Click the + button to add one!</p>';
                    return;
                }
                
                grid.innerHTML = cards.map(card => {
                    const themeKey = `${type}_${card.id}`;
                    const isDark = this.state.themes[themeKey] === 'dark';
                    const themeClass = isDark ? 'dark-theme' : '';
                    const themeIcon = isDark ? '☀️' : '🌙';
                    
                    return `
                        <div class="card ${themeClass}" data-id="${card.id}">
                            ${card.priority ? `<span class="priority-badge priority-${card.priority}">${card.priority === 'high' ? 'High Priority' : card.priority === 'medium' ? 'Medium' : 'Low'}</span>` : ''}
                            <button class="theme-toggle" onclick="App.toggleCardTheme('${type}', ${card.id})" title="Toggle theme">${themeIcon}</button>
                            <button class="del" onclick="App.deleteCard('${type}', ${card.id})">×</button>
                            <h3>${card.title}</h3>
                            ${card.desc ? `<p>${card.desc}</p>` : ''}
                            ${card.org ? `<div class="status-tags"><span class="status-tag tag-${card.org}">${card.org === 'at' ? 'AT' : card.org === 'ac' ? 'AC' : 'Integrated'}</span></div>` : ''}
                            ${type === 'milestones' && card.dueDate ? `<div style="margin-top:8px;font-size:0.85rem;color:#6b7280">📅 Due: ${new Date(card.dueDate).toLocaleDateString()}</div>` : ''}
                            ${card.drive ? `<div class="link-list"><a href="${card.drive}" target="_blank">📁 Drive Folder</a></div>` : ''}
                            ${card.links && card.links.length ? `<div class="link-list">${card.links.map(l => `<a href="${l}" target="_blank">${l}</a>`).join('')}</div>` : ''}
                            ${card.files && card.files.length ? `
                                <div class="file-list">
                                    <strong style="font-size:.85rem">📎 Documents (${card.files.length})</strong>
                                    ${card.files.map(f => `
                                        <div class="file-item">
                                            <div class="file-info">
                                                <span>${f.name}</span>
                                                ${f.inVault ? '<span class="vault-status">✓ In Vault</span>' : ''}
                                            </div>
                                            <div class="file-actions">
                                                ${!f.inVault ? `<button class="pill purple" onclick="App.moveFileToVault('${type}', ${card.id}, '${f.id}')">→ Vault</button>` : ''}
                                                <button class="pill red" onclick="App.removeFileFromCard('${type}', ${card.id}, '${f.id}')">Remove</button>
                                            </div>
                                        </div>
                                    `).join('')}
                                </div>
                            ` : ''}
                            <div class="actions">
                                <button class="pill blue" onclick="App.openModal('${type}', ${card.id})">✏️ Edit</button>
                                ${type === 'workstreams' || type === 'milestones' ? 
                                    `<button class="pill ${card.completed ? 'green' : 'yellow'}" onclick="App.toggleComplete('${type}', ${card.id})">
                                        ${card.completed ? '✓ Complete' : '○ In Progress'}
                                    </button>` : 
                                    '<button class="pill green">Active</button>'
                                }
                                <button class="pill gray">Updated ${new Date(card.updated).toLocaleDateString()}</button>
                            </div>
                        </div>
                    `;
                }).join('');
            });
        },

        // Update stats
        updateStats() {
            let totalItems = 0;
            let activeWorkstreams = 0;
            let upcomingMilestones = 0;
            let totalDocs = 0;

            ['overview', 'workstreams', 'milestones', 'resources'].forEach(type => {
                const cards = Object.values(this.state.cards[type] || {});
                totalItems += cards.length;
                
                if (type === 'workstreams') {
                    activeWorkstreams = cards.filter(c => !c.completed).length;
                }
                
                if (type === 'milestones') {
                    const now = new Date();
                    const thirtyDays = new Date(now.getTime() + 30 * 24 * 60 * 60 * 1000);
                    upcomingMilestones = cards.filter(c => {
                        if (c.dueDate) {
                            const due = new Date(c.dueDate);
                            return due >= now && due <= thirtyDays;
                        }
                        return false;
                    }).length;
                }
                
                cards.forEach(card => {
                    totalDocs += (card.files || []).length;
                });
            });

            document.getElementById('totalItems').textContent = totalItems;
            document.getElementById('activeWorkstreams').textContent = activeWorkstreams;
            document.getElementById('upcomingMilestones').textContent = upcomingMilestones;
            document.getElementById('totalDocuments').textContent = totalDocs;
            document.getElementById('vaultBadge').textContent = this.state.vault.length;
        },

        // Show notification
        showNotification(message, type = 'success') {
            const notif = document.getElementById('notification');
            notif.textContent = message;
            notif.style.background = type === 'error' ? '#ef4444' : '#10b981';
            notif.classList.add('show');
            setTimeout(() => notif.classList.remove('show'), 3000);
        },

        // Vault functions
        openVault() {
            document.getElementById('vaultOverlay').classList.add('show');
            
            const content = document.getElementById('vaultContent');
            content.innerHTML = `
                <div class="vault-empty">
                    <div class="vault-empty-icon">⏳</div>
                    <p>Loading vault...</p>
                </div>
            `;
            
            setTimeout(() => {
                this.renderCategories();
                this.renderVault();
                this.updateVaultStats();
                document.getElementById('vaultSearch').focus();
            }, 100);
        },

        closeVault() {
            const vault = document.getElementById('vaultOverlay');
            vault.classList.remove('show');
            vault.style.display = 'none';
            setTimeout(() => {
                vault.style.display = '';
            }, 10);
        },

        // Category functions
        renderCategories() {
            const tabs = document.getElementById('categoryTabs');
            tabs.innerHTML = `
                <div class="category-tab ${!this.state.currentCategory || this.state.currentCategory === 'all' ? 'active' : ''}" 
                     onclick="App.selectCategory('all')">
                    <span>All Files</span>
                </div>
            ` + this.state.vaultCategories.map(cat => `
                <div class="category-tab ${cat.id === this.state.currentCategory ? 'active' : ''}" 
                     onclick="App.selectCategory('${cat.id}')">
                    <span class="category-color" style="background: ${cat.color}"></span>
                    <span>${cat.name}</span>
                    ${cat.id !== 'general' ? `
                        <button class="category-menu-btn" onclick="event.stopPropagation(); App.showCategoryMenu('${cat.id}', event)">⋮</button>
                        <div class="category-menu" id="menu-${cat.id}">
                            <div class="category-menu-item" onclick="App.editCategory('${cat.id}')">✏️ Edit</div>
                            <div class="category-menu-item delete" onclick="App.deleteCategory('${cat.id}')">🗑️ Delete</div>
                        </div>
                    ` : ''}
                </div>
            `).join('');
        },

        showCategoryMenu(categoryId, event) {
            event.stopPropagation();
            // Close all other menus
            document.querySelectorAll('.category-menu').forEach(menu => menu.classList.remove('show'));
            // Toggle this menu
            const menu = document.getElementById(`menu-${categoryId}`);
            if (menu) {
                menu.classList.toggle('show');
            }
        },

        editCategory(categoryId) {
            const category = this.state.vaultCategories.find(c => c.id === categoryId);
            if (!category) return;

            this.state.editingCategoryId = categoryId;
            document.getElementById('editCategoryName').value = category.name;
            
            // Set color
            document.querySelectorAll('#editColorPicker .color-option').forEach(opt => {
                opt.classList.toggle('selected', opt.dataset.color === category.color);
            });

            document.getElementById('editCategoryOverlay').classList.add('show');
            document.getElementById('editCategoryName').focus();
            
            // Close menu
            document.querySelectorAll('.category-menu').forEach(menu => menu.classList.remove('show'));
        },

        closeEditCategoryModal() {
            document.getElementById('editCategoryOverlay').classList.remove('show');
            this.state.editingCategoryId = null;
        },

        updateCategory(e) {
            e.preventDefault();
            if (!this.state.editingCategoryId) return;

            const name = document.getElementById('editCategoryName').value.trim();
            const selectedColor = document.querySelector('#editColorPicker .color-option.selected');
            const color = selectedColor ? selectedColor.dataset.color : '#0066CC';

            if (name) {
                const categoryIndex = this.state.vaultCategories.findIndex(c => c.id === this.state.editingCategoryId);
                if (categoryIndex !== -1) {
                    this.state.vaultCategories[categoryIndex].name = name;
                    this.state.vaultCategories[categoryIndex].color = color;
                    this.saveData();
                    this.renderCategories();
                    this.closeEditCategoryModal();
                    this.showNotification('Category updated successfully');
                }
            }
        },

        deleteCategory(categoryId) {
            const category = this.state.vaultCategories.find(c => c.id === categoryId);
            if (!category) return;

            // Count files in this category
            const filesInCategory = this.state.vault.filter(f => f.category === categoryId).length;
            
            const confirmMsg = filesInCategory > 0 
                ? `Delete category "${category.name}"? ${filesInCategory} file(s) will be moved to General.`
                : `Delete category "${category.name}"?`;

            if (confirm(confirmMsg)) {
                // Move files to general category
                if (filesInCategory > 0) {
                    this.state.vault.forEach(file => {
                        if (file.category === categoryId) {
                            file.category = 'general';
                        }
                    });
                }

                // Remove category
                this.state.vaultCategories = this.state.vaultCategories.filter(c => c.id !== categoryId);
                
                // If current category was deleted, switch to all
                if (this.state.currentCategory === categoryId) {
                    this.state.currentCategory = 'all';
                }

                this.saveData();
                this.renderCategories();
                this.renderVault();
                this.updateVaultStats();
                this.showNotification('Category deleted');
            }
            
            // Close menu
            document.querySelectorAll('.category-menu').forEach(menu => menu.classList.remove('show'));
        },

        selectCategory(id) {
            this.state.currentCategory = id;
            this.saveData();
            this.renderCategories();
            this.renderVault();
            this.updateVaultStats();
        },

        showCategoryModal() {
            document.getElementById('categoryModalOverlay').classList.add('show');
            document.getElementById('categoryName').value = '';
            document.getElementById('categoryName').focus();
        },

        closeCategoryModal() {
            document.getElementById('categoryModalOverlay').classList.remove('show');
            // Reset form
            document.getElementById('categoryName').value = '';
            document.querySelectorAll('#colorPicker .color-option').forEach(o => o.classList.remove('selected'));
            document.querySelector('#colorPicker .color-option[data-color="#0066CC"]').classList.add('selected');
        },

        saveCategory(e) {
            e.preventDefault();
            const name = document.getElementById('categoryName').value.trim();
            const selectedColor = document.querySelector('.color-option.selected');
            const color = selectedColor ? selectedColor.dataset.color : '#0066CC';
            
            if (name) {
                // Check if category already exists
                const exists = this.state.vaultCategories.some(cat => 
                    cat.name.toLowerCase() === name.toLowerCase()
                );
                
                if (exists) {
                    this.showNotification('Category already exists', 'error');
                    return;
                }
                
                this.state.vaultCategories.push({
                    id: 'cat_' + Date.now(),
                    name,
                    color
                });
                this.saveData();
                this.renderCategories();
                this.closeCategoryModal();
                this.showNotification(`Category "${name}" added successfully`);
            }
        },

        getCategoryName(id) {
            const cat = this.state.vaultCategories.find(c => c.id === id);
            return cat ? cat.name : 'General';
        },

        // Document preview functions
        openDocument(fileId) {
            const file = this.state.vault.find(f => f.id === fileId);
            if (!file) return;

            const previewOverlay = document.getElementById('previewOverlay');
            const previewTitle = document.getElementById('previewTitle');
            const previewContent = document.getElementById('previewContent');

            previewTitle.textContent = file.name;
            previewOverlay.classList.add('show');

            const fileType = this.getFileType(file.name);
            const fileExt = file.name.split('.').pop().toLowerCase();

            if (fileType === 'html' && file.content) {
                // For HTML files, create a safe iframe with the content
                const iframe = document.createElement('iframe');
                iframe.className = 'preview-iframe';
                iframe.style.width = '100%';
                iframe.style.height = '600px';
                iframe.style.border = '1px solid #e5e7eb';
                iframe.style.borderRadius = '8px';
                iframe.style.background = '#fff';
                
                previewContent.innerHTML = '';
                previewContent.appendChild(iframe);
                
                // Write content to iframe
                const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
                iframeDoc.open();
                iframeDoc.write(file.content);
                iframeDoc.close();
            } else if (fileType === 'img' && file.dataUrl) {
                // For images, show directly
                previewContent.innerHTML = `
                    <div style="text-align:center;background:#fff;padding:20px;border-radius:8px;">
                        <img src="${file.dataUrl}" style="max-width:100%;max-height:600px;border-radius:8px;">
                    </div>
                `;
            } else if (fileType === 'pdf' && file.dataUrl) {
                // For PDF files, use embed or iframe
                previewContent.innerHTML = `
                    <div style="width:100%;height:600px;background:#fff;border-radius:8px;overflow:hidden;">
                        <embed src="${file.dataUrl}" type="application/pdf" width="100%" height="600px" />
                    </div>
                    <div style="text-align:center;margin-top:10px;">
                        <p style="color:#6b7280;font-size:14px;">If the PDF doesn't display, 
                        <a href="${file.dataUrl}" download="${file.name}" style="color:#2563eb;text-decoration:underline;">click here to download</a></p>
                    </div>
                `;
            } else if ((fileType === 'doc' || fileExt === 'docx') && file.dataUrl) {
                // For Word documents, provide download and info
                previewContent.innerHTML = `
                    <div style="text-align:center;padding:60px;background:#fff;border-radius:8px;">
                        <div style="font-size:4rem;margin-bottom:20px;">📄</div>
                        <h3 style="color:#1f2937;margin-bottom:16px;">${file.name}</h3>
                        <div style="color:#6b7280;line-height:1.8;">
                            <p>Microsoft Word Document</p>
                            <p>Size: ${this.formatFileSize(file.size || 0)}</p>
                            <p>Added: ${new Date(file.date).toLocaleDateString()}</p>
                            ${file.source ? `<p>Source: ${file.source}</p>` : ''}
                        </div>
                        <div style="margin-top:30px;">
                            <button class="btn" style="background:#2563eb;color:#fff;margin-right:10px" 
                                    onclick="App.downloadFile('${fileId}')">
                                📥 Download Document
                            </button>
                            <button class="btn" style="background:#10b981;color:#fff" 
                                    onclick="window.open('https://docs.google.com/viewer?url=' + encodeURIComponent('${file.dataUrl}'), '_blank')">
                                🌐 Open in Google Docs Viewer
                            </button>
                        </div>
                        <p style="color:#6b7280;font-size:12px;margin-top:20px;">
                            Word documents cannot be displayed directly. Download to view in Microsoft Word or use Google Docs Viewer.
                        </p>
                    </div>
                `;
            } else if ((fileType === 'xls' || fileExt === 'xlsx') && file.dataUrl) {
                // For Excel files
                previewContent.innerHTML = `
                    <div style="text-align:center;padding:60px;background:#fff;border-radius:8px;">
                        <div style="font-size:4rem;margin-bottom:20px;">📊</div>
                        <h3 style="color:#1f2937;margin-bottom:16px;">${file.name}</h3>
                        <div style="color:#6b7280;line-height:1.8;">
                            <p>Microsoft Excel Spreadsheet</p>
                            <p>Size: ${this.formatFileSize(file.size || 0)}</p>
                            <p>Added: ${new Date(file.date).toLocaleDateString()}</p>
                            ${file.source ? `<p>Source: ${file.source}</p>` : ''}
                        </div>
                        <button class="btn" style="margin-top:20px;background:#2563eb;color:#fff" 
                                onclick="App.downloadFile('${fileId}')">
                            📥 Download Spreadsheet
                        </button>
                    </div>
                `;
            } else if ((fileType === 'doc' || file.type.startsWith('text/')) && file.content) {
                // For text files, show content
                previewContent.innerHTML = `
                    <div class="preview-text">${this.escapeHtml(file.content)}</div>
                `;
            } else {
                // For other files, show info and download option
                previewContent.innerHTML = `
                    <div style="text-align:center;padding:60px;background:#fff;border-radius:8px;">
                        <div style="font-size:4rem;margin-bottom:20px;">${this.getFileIcon(fileType)}</div>
                        <h3 style="color:#1f2937;margin-bottom:16px;">${file.name}</h3>
                        <div style="color:#6b7280;line-height:1.8;">
                            <p>File type: ${fileExt.toUpperCase()}</p>
                            <p>Size: ${this.formatFileSize(file.size || 0)}</p>
                            <p>Added: ${new Date(file.date).toLocaleDateString()}</p>
                            ${file.source ? `<p>Source: ${file.source}</p>` : ''}
                        </div>
                        <button class="btn" style="margin-top:20px;background:#2563eb;color:#fff" 
                                onclick="App.downloadFile('${fileId}')">
                            📥 Download File
                        </button>
                    </div>
                `;
            }
        },

        closePreview() {
            const preview = document.getElementById('previewOverlay');
            preview.classList.remove('show');
            preview.style.display = 'none';
            setTimeout(() => {
                preview.style.display = '';
            }, 10);
        },

        escapeHtml(text) {
            const map = {
                '&': '&amp;',
                '<': '&lt;',
                '>': '&gt;',
                '"': '&quot;',
                "'": '&#039;'
            };
            return String(text).replace(/[&<>"']/g, m => map[m]);
        },

        searchVault() {
            this.state.vaultSearchTerm = document.getElementById('vaultSearch').value.toLowerCase();
            document.getElementById('searchClear').style.display = this.state.vaultSearchTerm ? 'flex' : 'none';
            this.renderVault();
        },

        clearSearch() {
            document.getElementById('vaultSearch').value = '';
            this.state.vaultSearchTerm = '';
            document.getElementById('searchClear').style.display = 'none';
            this.renderVault();
        },

        filterVault() {
            this.state.currentVaultFilter = document.getElementById('vaultFilter').value;
            this.renderVault();
        },

        sortVault() {
            this.state.currentVaultSort = document.getElementById('vaultSort').value;
            this.renderVault();
        },

        getFileType(filename) {
            const ext = filename.split('.').pop().toLowerCase();
            if (['pdf'].includes(ext)) return 'pdf';
            if (['doc', 'docx', 'txt'].includes(ext)) return 'doc';
            if (['xls', 'xlsx', 'csv'].includes(ext)) return 'xls';
            if (['jpg', 'jpeg', 'png', 'gif', 'bmp'].includes(ext)) return 'img';
            if (['html', 'htm'].includes(ext)) return 'html';
            return 'other';
        },

        getFileIcon(type) {
            switch(type) {
                case 'pdf': return '📄';
                case 'doc': return '📝';
                case 'xls': return '📊';
                case 'img': return '🖼️';
                case 'html': return '🌐';
                default: return '📎';
            }
        },

        formatFileSize(bytes) {
            if (bytes < 1024) return bytes + ' B';
            if (bytes < 1024 * 1024) return (bytes / 1024).toFixed(1) + ' KB';
            return (bytes / (1024 * 1024)).toFixed(1) + ' MB';
        },

        updateVaultStats() {
            const total = this.state.vault.length;
            const totalSize = this.state.vault.reduce((sum, file) => sum + (file.size || 0), 0);
            
            const oneWeekAgo = new Date();
            oneWeekAgo.setDate(oneWeekAgo.getDate() - 7);
            const recent = this.state.vault.filter(file => new Date(file.date) > oneWeekAgo).length;

            // Count files in current category
            let categoryCount = 0;
            if (this.state.currentCategory && this.state.currentCategory !== 'all') {
                categoryCount = this.state.vault.filter(f => f.category === this.state.currentCategory).length;
            } else {
                categoryCount = total;
            }

            document.getElementById('vaultTotal').textContent = total;
            document.getElementById('vaultSize').textContent = this.formatFileSize(totalSize);
            document.getElementById('vaultRecent').textContent = recent;
            document.getElementById('categoryCount').textContent = categoryCount;
            
            const clearBtn = document.getElementById('clearVaultBtn');
            if (clearBtn) {
                clearBtn.disabled = total === 0;
                clearBtn.style.background = total === 0 ? '#6b7280' : '#dc2626';
            }
        },

        renderVault() {
            const content = document.getElementById('vaultContent');
            let files = [...this.state.vault];

            // Apply category filter
            if (this.state.currentCategory && this.state.currentCategory !== 'all') {
                files = files.filter(file => file.category === this.state.currentCategory);
            }

            // Apply search filter
            if (this.state.vaultSearchTerm) {
                files = files.filter(file => 
                    file.name.toLowerCase().includes(this.state.vaultSearchTerm) ||
                    (file.source && file.source.toLowerCase().includes(this.state.vaultSearchTerm))
                );
            }

            // Apply type filter
            if (this.state.currentVaultFilter !== 'all') {
                files = files.filter(file => this.getFileType(file.name) === this.state.currentVaultFilter);
            }

            // Apply sort
            files.sort((a, b) => {
                switch(this.state.currentVaultSort) {
                    case 'date-desc': return new Date(b.date) - new Date(a.date);
                    case 'date-asc': return new Date(a.date) - new Date(b.date);
                    case 'name-asc': return a.name.localeCompare(b.name);
                    case 'name-desc': return b.name.localeCompare(a.name);
                    case 'size-desc': return (b.size || 0) - (a.size || 0);
                    case 'size-asc': return (a.size || 0) - (b.size || 0);
                    default: return 0;
                }
            });

            const hasActiveFilters = this.state.vaultSearchTerm || this.state.currentVaultFilter !== 'all';
            const filterStatus = hasActiveFilters ? 
                `<div style="display:flex;align-items:center;justify-content:center;gap:12px;padding:10px;background:#f3f4f6;border-radius:8px;margin-bottom:16px;font-size:0.9rem;color:#6b7280">
                    <span>
                        Showing ${files.length} of ${this.state.vault.length} files
                        ${this.state.vaultSearchTerm ? ` matching "${this.state.vaultSearchTerm}"` : ''}
                        ${this.state.currentVaultFilter !== 'all' ? ` (${this.state.currentVaultFilter} files only)` : ''}
                    </span>
                    <button class="pill gray" onclick="App.resetFilters()">Reset Filters</button>
                </div>` : '';

            if (files.length === 0) {
                content.innerHTML = filterStatus + `
                    <div class="vault-empty">
                        <div class="vault-empty-icon">📂</div>
                        <p>${hasActiveFilters ? 'No files match your search criteria' : 'No documents in vault yet'}</p>
                        <p style="font-size:0.9rem;margin-top:8px;color:#6b7280">
                            ${hasActiveFilters ? 'Try adjusting your filters or search term' : 'Move documents to vault from any workspace item'}
                        </p>
                    </div>
                `;
            } else {
                content.innerHTML = filterStatus + files.map(file => {
                    const fileType = this.getFileType(file.name);
                    const icon = this.getFileIcon(fileType);
                    const category = this.state.vaultCategories.find(c => c.id === file.category);
                    
                    return `
                        <div class="vault-item" onclick="App.openDocument('${file.id}')" style="cursor:pointer">
                            <div class="vault-item-icon ${fileType}">${icon}</div>
                            <div class="vault-item-info">
                                <div class="vault-item-name">${file.name}</div>
                                <div class="vault-item-meta">
                                    <span>📅 ${new Date(file.date).toLocaleDateString()}</span>
                                    <span>💾 ${this.formatFileSize(file.size || 0)}</span>
                                    <span>📍 ${file.source || 'Unknown source'}</span>
                                    ${category ? `<span style="color:${category.color}">● ${category.name}</span>` : ''}
                                </div>
                            </div>
                            <div class="vault-item-actions" onclick="event.stopPropagation()">
                                <button class="pill blue" onclick="App.downloadFile('${file.id}')">📥 Download</button>
                                <button class="pill red" onclick="App.removeFromVault('${file.id}')">Remove</button>
                            </div>
                        </div>
                    `;
                }).join('');
            }
        },

        resetFilters() {
            this.clearSearch();
            document.getElementById('vaultFilter').value = 'all';
            document.getElementById('vaultSort').value = 'date-desc';
            this.state.currentVaultFilter = 'all';
            this.state.currentVaultSort = 'date-desc';
            this.renderVault();
        },

        downloadFile(fileId) {
            const file = this.state.vault.find(f => f.id === fileId);
            if (!file) {
                this.showNotification('File not found', 'error');
                return;
            }

            try {
                // Create download link
                const link = document.createElement('a');
                link.download = file.name;

                if (file.dataUrl) {
                    // If we have a data URL, use it directly
                    link.href = file.dataUrl;
                } else if (file.content) {
                    // If we have text content, create a blob
                    const blob = new Blob([file.content], { type: file.type || 'text/plain' });
                    link.href = URL.createObjectURL(blob);
                } else if (file.base64) {
                    // If we have base64 data, convert it
                    const byteCharacters = atob(file.base64);
                    const byteNumbers = new Array(byteCharacters.length);
                    for (let i = 0; i < byteCharacters.length; i++) {
                        byteNumbers[i] = byteCharacters.charCodeAt(i);
                    }
                    const byteArray = new Uint8Array(byteNumbers);
                    const blob = new Blob([byteArray], { type: file.type || 'application/octet-stream' });
                    link.href = URL.createObjectURL(blob);
                } else {
                    this.showNotification('File data not available for download', 'error');
                    return;
                }

                // Trigger download
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);

                // Clean up object URL if created
                if (link.href.startsWith('blob:')) {
                    setTimeout(() => URL.revokeObjectURL(link.href), 100);
                }

                this.showNotification(`Downloading ${file.name}...`);
            } catch (error) {
                console.error('Download error:', error);
                this.showNotification('Failed to download file', 'error');
            }
        },

        // HTML Display Functions
        openHtmlPasteModal() {
            document.getElementById('htmlPasteOverlay').classList.add('show');
            document.getElementById('htmlTitle').value = '';
            document.getElementById('htmlContent').value = '';
            document.getElementById('htmlTitle').focus();
        },

        closeHtmlPasteModal() {
            const modal = document.getElementById('htmlPasteOverlay');
            modal.classList.remove('show');
            modal.style.display = 'none';
            setTimeout(() => {
                modal.style.display = '';
            }, 10);
        },

        saveHtmlContent(e) {
            e.preventDefault();
            const title = document.getElementById('htmlTitle').value.trim();
            const content = document.getElementById('htmlContent').value.trim();
            
            if (title && content) {
                // Initialize htmlDisplayItems array if it doesn't exist
                if (!this.state.htmlDisplayItems) {
                    this.state.htmlDisplayItems = [];
                }
                
                const newItem = {
                    id: 'html_' + Date.now(),
                    title: title,
                    content: content,
                    created: new Date().toISOString(),
                    order: this.state.htmlDisplayItems.length
                };
                
                this.state.htmlDisplayItems.push(newItem);
                this.saveData();
                this.renderHtmlItems();
                this.closeHtmlPasteModal();
                this.showNotification('HTML content added successfully');
                
                // Debug log
                console.log('Saved HTML items:', this.state.htmlDisplayItems);
            }
        },

        renderHtmlItems() {
            const container = document.getElementById('htmlItemsContainer');
            if (!container) return;
            
            // Debug log
            console.log('Rendering HTML items:', this.state.htmlDisplayItems);
            
            if (!this.state.htmlDisplayItems || this.state.htmlDisplayItems.length === 0) {
                container.innerHTML = `
                    <div class="html-empty-state">
                        <div class="html-empty-icon">📄</div>
                        <p>No HTML content yet. Click "Add HTML" to paste your first HTML file.</p>
                    </div>
                `;
                return;
            }
            
            // Sort by order
            const sortedItems = [...this.state.htmlDisplayItems].sort((a, b) => a.order - b.order);
            
            container.innerHTML = sortedItems.map((item, index) => `
                <div class="html-item" data-id="${item.id}">
                    <div class="html-item-header">
                        <div class="html-item-title">${this.escapeHtml(item.title)}</div>
                        <div class="html-item-controls">
                            <button class="html-control-btn fullscreen" 
                                    onclick="App.openHtmlFullscreen('${item.id}')">
                                ⛶ Fullscreen
                            </button>
                            <button class="html-control-btn move-up" 
                                    onclick="App.moveHtmlItem('${item.id}', 'up')"
                                    ${index === 0 ? 'disabled' : ''}>
                                ↑ Up
                            </button>
                            <button class="html-control-btn move-down" 
                                    onclick="App.moveHtmlItem('${item.id}', 'down')"
                                    ${index === sortedItems.length - 1 ? 'disabled' : ''}>
                                ↓ Down
                            </button>
                            <button class="html-control-btn delete" 
                                    onclick="App.deleteHtmlItem('${item.id}')">
                                🗑️ Delete
                            </button>
                        </div>
                    </div>
                    <iframe class="html-content-frame" 
                            id="frame-${item.id}"
                            sandbox="allow-same-origin allow-scripts"
                            style="width:100%;border:1px solid var(--border-primary);border-radius:6px;background:var(--bg-card);"></iframe>
                </div>
            `).join('');
            
            // Load content into iframes with error handling
            sortedItems.forEach(item => {
                const iframe = document.getElementById(`frame-${item.id}`);
                if (iframe && item.content) {
                    try {
                        const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
                        iframeDoc.open();
                        iframeDoc.write(item.content);
                        iframeDoc.close();
                        
                        // Auto-resize iframe based on content
                        iframe.onload = () => {
                            try {
                                const height = iframe.contentDocument.body.scrollHeight;
                                iframe.style.height = Math.max(300, height + 20) + 'px';
                            } catch (e) {
                                iframe.style.height = '400px';
                            }
                        };
                    } catch (e) {
                        console.error('Error loading HTML content into iframe:', e);
                        iframe.style.height = '400px';
                    }
                }
            });
        },

        moveHtmlItem(itemId, direction) {
            const items = [...this.state.htmlDisplayItems].sort((a, b) => a.order - b.order);
            const currentIndex = items.findIndex(item => item.id === itemId);
            
            if (currentIndex === -1) return;
            
            if (direction === 'up' && currentIndex > 0) {
                // Swap orders
                const temp = items[currentIndex].order;
                items[currentIndex].order = items[currentIndex - 1].order;
                items[currentIndex - 1].order = temp;
            } else if (direction === 'down' && currentIndex < items.length - 1) {
                // Swap orders
                const temp = items[currentIndex].order;
                items[currentIndex].order = items[currentIndex + 1].order;
                items[currentIndex + 1].order = temp;
            }
            
            this.saveData();
            this.renderHtmlItems();
        },

        deleteHtmlItem(itemId) {
            if (confirm('Delete this HTML content?')) {
                this.state.htmlDisplayItems = this.state.htmlDisplayItems.filter(item => item.id !== itemId);
                
                // Reorder remaining items
                this.state.htmlDisplayItems.sort((a, b) => a.order - b.order);
                this.state.htmlDisplayItems.forEach((item, index) => {
                    item.order = index;
                });
                
                this.saveData();
                this.renderHtmlItems();
                this.showNotification('HTML content deleted');
            }
        },

        openHtmlFullscreen(itemId) {
            const item = this.state.htmlDisplayItems.find(i => i.id === itemId);
            if (!item) return;

            const overlay = document.getElementById('htmlFullscreenOverlay');
            const iframe = document.getElementById('fullscreenIframe');
            const title = document.getElementById('fullscreenTitle');

            title.textContent = item.title;
            overlay.classList.add('show');

            // Load content into fullscreen iframe
            const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
            iframeDoc.open();
            iframeDoc.write(item.content);
            iframeDoc.close();

            // Store current item ID for reference
            this.currentFullscreenItemId = itemId;
        },

        closeHtmlFullscreen() {
            const overlay = document.getElementById('htmlFullscreenOverlay');
            overlay.classList.remove('show');
            this.currentFullscreenItemId = null;
        },

        toggleFullscreenMode() {
            const iframe = document.getElementById('fullscreenIframe');
            
            if (!document.fullscreenElement) {
                // Enter browser fullscreen
                if (iframe.requestFullscreen) {
                    iframe.requestFullscreen();
                } else if (iframe.webkitRequestFullscreen) {
                    iframe.webkitRequestFullscreen();
                } else if (iframe.msRequestFullscreen) {
                    iframe.msRequestFullscreen();
                }
            } else {
                // Exit browser fullscreen
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                } else if (document.msExitFullscreen) {
                    document.msExitFullscreen();
                }
            }
        },

        removeFromVault(fileId) {
            const file = this.state.vault.find(f => f.id === fileId);
            if (file && confirm(`Remove "${file.name}" from vault?`)) {
                this.state.vault = this.state.vault.filter(f => f.id !== fileId);
                
                // Update the original card's file status
                ['overview', 'workstreams', 'milestones', 'resources'].forEach(type => {
                    Object.values(this.state.cards[type] || {}).forEach(card => {
                        if (card.files) {
                            card.files.forEach(f => {
                                if (f.id === fileId) {
                                    f.inVault = false;
                                }
                            });
                        }
                    });
                });
                
                this.saveData();
                this.renderVault();
                this.updateVaultStats();
                this.renderCards();
                this.showNotification(`Removed "${file.name}" from vault`);
                
                // Update vault badge
                document.getElementById('vaultBadge').textContent = this.state.vault.length;
            }
        },

        exportVaultList() {
            const vaultData = this.state.vault.map(file => ({
                name: file.name,
                date: new Date(file.date).toLocaleDateString(),
                size: this.formatFileSize(file.size || 0),
                source: file.source || 'Unknown',
                type: this.getFileType(file.name)
            }));
            
            const csvContent = 'data:text/csv;charset=utf-8,' + 
                'Name,Date Added,Size,Source,Type\n' +
                vaultData.map(f => `"${f.name}","${f.date}","${f.size}","${f.source}","${f.type}"`).join('\n');
            
            const link = document.createElement('a');
            link.setAttribute('href', encodeURI(csvContent));
            link.setAttribute('download', `vault_export_${new Date().toISOString().split('T')[0]}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            this.showNotification('Vault list exported as CSV');
        },

        clearVault() {
            if (this.state.vault.length === 0) {
                this.showNotification('Vault is already empty');
                return;
            }
            
            if (confirm(`Are you sure you want to remove all ${this.state.vault.length} files from the vault? This action cannot be undone.`)) {
                // Update all cards to reflect files no longer in vault
                this.state.vault.forEach(vaultFile => {
                    ['overview', 'workstreams', 'milestones', 'resources'].forEach(type => {
                        Object.values(this.state.cards[type] || {}).forEach(card => {
                            if (card.files) {
                                card.files.forEach(f => {
                                    if (f.id === vaultFile.id) {
                                        f.inVault = false;
                                    }
                                });
                            }
                        });
                    });
                });
                
                this.state.vault = [];
                this.saveData();
                this.renderVault();
                this.updateVaultStats();
                this.renderCards();
                this.showNotification('Vault cleared successfully');
                
                // Update vault badge
                document.getElementById('vaultBadge').textContent = '0';
            }
        }
    };

    // Initialize app when DOM is ready
    document.addEventListener('DOMContentLoaded', () => App.init());
    </script>
</body>
</html>
