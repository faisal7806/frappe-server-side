```
Exception translatable (#3473)
M	frappe/client.py
M	frappe/public/js/frappe/desk.js

[minor] print output if login fails
M	frappe/frappeclient.py

[fix] Enqueue syncing global search (#3455)
M	frappe/database.py
M	frappe/model/document.py
M	frappe/utils/global_search.py

Jinja translations for website (#3483)
M	frappe/templates/includes/comments/comments.html
M	frappe/templates/includes/contact.js
M	frappe/templates/includes/login/login.js

Batch/Serial Number entry modal (#3298)
M	frappe/public/js/frappe/form/control.js
M	frappe/public/js/frappe/form/grid.js

Add icon for Deleted Documents
M	frappe/config/setup.py

fixed module for address
M	frappe/hooks.py

[PDF] Wrap long text (frappe/erpnext#9107)
M	frappe/templates/styles/standard.css

[minor][fix] check boot.systemdefaults too
M	frappe/public/js/frappe/misc/number_format.js

[minor] print_template and frappe.render_grid fixes (#3476)
M	frappe/public/js/frappe/views/reports/query_report.js
M	frappe/public/js/lib/microtemplate.js

Minor issue when generating the pdf for the reports having html format (#3478)
M	frappe/public/js/frappe/views/reports/query_report.js

[fix] genders patch
M	frappe/patches/v8_0/update_gender_and_salutation.py

Configurable error traceback (#3464)
M	frappe/core/doctype/system_settings/system_settings.json
A	frappe/patches/v8_0/set_allow_traceback.py
M	frappe/utils/response.py

[translation] translation updates (#3471)
M	frappe/translations/ar.csv
M	frappe/translations/da.csv
M	frappe/translations/de.csv
M	frappe/translations/es.csv
M	frappe/translations/fr.csv
M	frappe/translations/it.csv
M	frappe/translations/pt-BR.csv
M	frappe/translations/uk.csv
M	frappe/translations/vi.csv

Salutation and Gender in Contact (#3079)
M	frappe/config/desktop.py
R100	frappe/email/doctype/contact/__init__.py	frappe/contacts/__init__.py
R097	frappe/geo/address_and_contact.py	frappe/contacts/address_and_contact.py
R100	frappe/geo/doctype/address/__init__.py	frappe/contacts/doctype/__init__.py
R100	frappe/geo/doctype/address_template/__init__.py	frappe/contacts/doctype/address/__init__.py
R092	frappe/geo/doctype/address/address.js	frappe/contacts/doctype/address/address.js
R099	frappe/geo/doctype/address/address.json	frappe/contacts/doctype/address/address.json
R100	frappe/geo/doctype/address/address.py	frappe/contacts/doctype/address/address.py
A	frappe/contacts/doctype/address/test_address.py
R100	frappe/geo/report/addresses_and_contacts/__init__.py	frappe/contacts/doctype/address_template/__init__.py
R079	frappe/geo/doctype/address_template/address_template.js	frappe/contacts/doctype/address_template/address_template.js
R094	frappe/geo/doctype/address_template/address_template.json	frappe/contacts/doctype/address_template/address_template.json
R100	frappe/geo/doctype/address_template/address_template.py	frappe/contacts/doctype/address_template/address_template.py
A	frappe/contacts/doctype/address_template/test_address_template.py
A	frappe/contacts/doctype/contact/__init__.py
R095	frappe/email/doctype/contact/contact.js	frappe/contacts/doctype/contact/contact.js
R091	frappe/email/doctype/contact/contact.json	frappe/contacts/doctype/contact/contact.json
R100	frappe/email/doctype/contact/contact.py	frappe/contacts/doctype/contact/contact.py
R077	frappe/email/doctype/contact/test_contact.py	frappe/contacts/doctype/contact/test_contact.py
R100	frappe/email/doctype/contact/test_records.json	frappe/contacts/doctype/contact/test_records.json
A	frappe/contacts/doctype/gender/__init__.py
A	frappe/contacts/doctype/gender/gender.js
A	frappe/contacts/doctype/gender/gender.json
A	frappe/contacts/doctype/gender/gender.py
A	frappe/contacts/doctype/gender/test_gender.py
A	frappe/contacts/doctype/salutation/__init__.py
A	frappe/contacts/doctype/salutation/salutation.js
A	frappe/contacts/doctype/salutation/salutation.json
A	frappe/contacts/doctype/salutation/salutation.py
A	frappe/contacts/doctype/salutation/test_salutation.py
A	frappe/contacts/report/__init__.py
A	frappe/contacts/report/addresses_and_contacts/__init__.py
R100	frappe/geo/report/addresses_and_contacts/addresses_and_contacts.js	frappe/contacts/report/addresses_and_contacts/addresses_and_contacts.js
R088	frappe/geo/report/addresses_and_contacts/addresses_and_contacts.json	frappe/contacts/report/addresses_and_contacts/addresses_and_contacts.json
R100	frappe/geo/report/addresses_and_contacts/addresses_and_contacts.py	frappe/contacts/report/addresses_and_contacts/addresses_and_contacts.py
A	frappe/desk/page/setup_wizard/install_fixtures.py
M	frappe/desk/page/setup_wizard/setup_wizard.py
D	frappe/geo/doctype/address/test_address.py
D	frappe/geo/doctype/address/test_records.json
D	frappe/geo/doctype/address_template/test_address_template.py
D	frappe/geo/doctype/address_template/test_records.json
M	frappe/hooks.py
M	frappe/modules.txt
M	frappe/patches.txt
A	frappe/patches/v8_0/update_gender_and_salutation.py
M	frappe/public/js/frappe/misc/address_and_contact.js

GSuite integration (#3252)
M	frappe/boot.py
M	frappe/config/integrations.py
A	frappe/docs/user/en/guides/integration/google_gsuite.md
M	frappe/docs/user/en/guides/integration/index.txt
A	frappe/integrations/doctype/gsuite_settings/__init__.py
A	frappe/integrations/doctype/gsuite_settings/gsuite_settings.js
A	frappe/integrations/doctype/gsuite_settings/gsuite_settings.json
A	frappe/integrations/doctype/gsuite_settings/gsuite_settings.py
A	frappe/integrations/doctype/gsuite_templates/__init__.py
A	frappe/integrations/doctype/gsuite_templates/gsuite_templates.js
A	frappe/integrations/doctype/gsuite_templates/gsuite_templates.json
A	frappe/integrations/doctype/gsuite_templates/gsuite_templates.py
A	frappe/integrations/doctype/gsuite_templates/test_gsuite_templates.py
M	frappe/public/build.json
M	frappe/public/js/frappe/form/footer/attachments.js
M	frappe/public/js/frappe/upload.js
A	frappe/public/js/integrations/gsuite.js

Added columns field (#3469)
M	frappe/custom/doctype/custom_field/custom_field.json

[feature] domainification for frappe (#3227)
M	frappe/__init__.py
M	frappe/boot.py
M	frappe/core/doctype/doctype/doctype.json
M	frappe/core/doctype/doctype/test_doctype.py
A	frappe/core/doctype/domain/__init__.py
A	frappe/core/doctype/domain/domain.js
A	frappe/core/doctype/domain/domain.json
A	frappe/core/doctype/domain/domain.py
A	frappe/core/doctype/domain/test_domain.py
A	frappe/core/doctype/domain_settings/__init__.py
A	frappe/core/doctype/domain_settings/domain_settings.js
A	frappe/core/doctype/domain_settings/domain_settings.json
A	frappe/core/doctype/domain_settings/domain_settings.py
A	frappe/core/doctype/has_domain/__init__.py
A	frappe/core/doctype/has_domain/has_domain.json
A	frappe/core/doctype/has_domain/has_domain.py
M	frappe/core/doctype/page/page.json
M	frappe/core/doctype/role/role.json
M	frappe/core/doctype/user/user.py
M	frappe/core/page/permission_manager/permission_manager.py
M	frappe/custom/doctype/customize_form/customize_form.js
M	frappe/desk/doctype/desktop_icon/desktop_icon.py
M	frappe/desk/moduleview.py
M	frappe/public/build.json
A	frappe/public/js/frappe/checkbox_editor.js
A	frappe/tests/test_domainification.py

several throw translations (#3441)
M	frappe/commands/site.py
M	frappe/core/doctype/file/file_list.js
M	frappe/core/doctype/user/user.py
M	frappe/desk/doctype/bulk_update/bulk_update.py
M	frappe/desk/doctype/desktop_icon/desktop_icon.py
M	frappe/desk/page/applications/applications.py
M	frappe/desk/search.py
M	frappe/email/doctype/email_alert/email_alert.py
M	frappe/email/doctype/email_domain/email_domain.py
M	frappe/integrations/doctype/ldap_settings/ldap_settings.py
M	frappe/integrations/doctype/paypal_settings/paypal_settings.py
M	frappe/utils/background_jobs.py
M	frappe/utils/data.py
M	frappe/www/feedback.py

Add Arabic translation for datepicker (#3453)
M	frappe/public/js/lib/datepicker/locale-all.js

Better error message for duplicate desktop icon (#3446)
M	frappe/desk/doctype/desktop_icon/desktop_icon.py

Create hooks.md
M	frappe/docs/user/en/guides/basics/hooks.md

[enhance] make bench commands extensible by apps (#3457)
M	frappe/commands/site.py
M	frappe/utils/bench_helper.py

Fix frappe/erpnext#9115 (#3449)
M	frappe/public/js/lib/frappe-gantt/frappe-gantt.js

Make 'By' translatable in blog posts (#3450)
M	frappe/website/doctype/blog_post/templates/blog_post.html
M	frappe/website/doctype/blog_post/templates/blog_post_row.html

Add inList
M	frappe/public/js/frappe/misc/number_format.js

Add proxy variables for removed globals
M	frappe/public/js/frappe/desk.js
M	frappe/public/js/frappe/misc/datetime.js
M	frappe/public/js/frappe/ui/messages.js
M	frappe/public/js/legacy/datatype.js
M	frappe/public/js/legacy/form.js
M	frappe/public/js/legacy/globals.js

Missing `+` operator
M	frappe/docs/user/en/guides/app-development/dialogs-types.md

Email parse addr fix. (#3371)
M	frappe/core/doctype/communication/test_communication.py
M	frappe/utils/__init__.py

[translation] translation updates (#3439)
M	frappe/translations/am.csv
M	frappe/translations/ar.csv
M	frappe/translations/bg.csv
M	frappe/translations/bn.csv
M	frappe/translations/bs.csv
M	frappe/translations/ca.csv
M	frappe/translations/cs.csv
M	frappe/translations/da.csv
M	frappe/translations/de.csv
M	frappe/translations/el.csv
M	frappe/translations/es-AR.csv
M	frappe/translations/es-CL.csv
M	frappe/translations/es-PE.csv
M	frappe/translations/es.csv
M	frappe/translations/et.csv
M	frappe/translations/fa.csv
M	frappe/translations/fi.csv
M	frappe/translations/fr.csv
M	frappe/translations/gu.csv
M	frappe/translations/he.csv
M	frappe/translations/hi.csv
M	frappe/translations/hr.csv
M	frappe/translations/hu.csv
M	frappe/translations/id.csv
M	frappe/translations/is.csv
M	frappe/translations/it.csv
M	frappe/translations/ja.csv
M	frappe/translations/km.csv
M	frappe/translations/kn.csv
M	frappe/translations/ko.csv
M	frappe/translations/ku.csv
M	frappe/translations/lo.csv
M	frappe/translations/lt.csv
M	frappe/translations/lv.csv
M	frappe/translations/mk.csv
M	frappe/translations/ml.csv
M	frappe/translations/mr.csv
M	frappe/translations/ms.csv
M	frappe/translations/my.csv
M	frappe/translations/nl.csv
M	frappe/translations/no.csv
M	frappe/translations/pl.csv
M	frappe/translations/ps.csv
M	frappe/translations/pt-BR.csv
M	frappe/translations/pt.csv
M	frappe/translations/ro.csv
M	frappe/translations/ru.csv
M	frappe/translations/si.csv
M	frappe/translations/sk.csv
M	frappe/translations/sl.csv
M	frappe/translations/sq.csv
M	frappe/translations/sr.csv
M	frappe/translations/sv.csv
M	frappe/translations/ta.csv
M	frappe/translations/te.csv
M	frappe/translations/th.csv
M	frappe/translations/tr.csv
M	frappe/translations/uk.csv
M	frappe/translations/ur.csv
M	frappe/translations/vi.csv
M	frappe/translations/zh-TW.csv
M	frappe/translations/zh.csv

Set camelcase to off
M	.eslintrc

translation errors in several msgprint (#3438)
M	frappe/core/doctype/deleted_document/deleted_document.py
M	frappe/core/doctype/feedback_trigger/feedback_trigger.py
M	frappe/core/doctype/file/file.py
M	frappe/installer.py
M	frappe/modules/utils.py
M	frappe/public/js/frappe/list/list_view.js
M	frappe/public/js/frappe/misc/utils.js
M	frappe/public/js/frappe/views/image/image_view.js
M	frappe/public/js/legacy/clientscriptAPI.js
M	frappe/templates/includes/comments/comments.html
M	frappe/www/update-password.html

Remove testcafe folder
D	frappe/tests/testcafe/0-test_setup_wizard.js
D	frappe/tests/testcafe/test_todo.js
D	frappe/tests/testcafe/uploads/user_picture.svg

Remove testcafe from travis
M	.travis.yml

[minor] removed global variable user from navbar.html
M	frappe/public/js/frappe/ui/toolbar/navbar.html

fix RTL issues in tree view
M	frappe/public/css/desk-rtl.css

Global Date Format Localisation (#3428)
M	frappe/utils/data.py

minor
M	frappe/public/js/frappe/form/control.js

Fix build.js
M	frappe/build.js

Fix summernote ul/ol issue
M	frappe/public/js/frappe/form/control.js

Added console.warn messages for deprecated API
M	frappe/public/js/frappe/desk.js
M	frappe/public/js/frappe/misc/datetime.js
M	frappe/public/js/frappe/ui/messages.js
M	frappe/public/js/legacy/datatype.js
M	frappe/public/js/legacy/form.js

add toString method to frappe.user
M	frappe/public/js/frappe/misc/user.js

Added files in .eslintignore, updated globals
M	.eslintignore
M	.eslintrc
M	frappe/build.js
M	frappe/core/doctype/communication/communication_list.js
M	frappe/core/doctype/doctype/boilerplate/controller_list.js
M	frappe/core/doctype/doctype/doctype.js
M	frappe/core/doctype/error_log/error_log_list.js
M	frappe/core/doctype/error_snapshot/error_snapshot.js
M	frappe/core/doctype/error_snapshot/error_snapshot_list.js
M	frappe/core/doctype/feedback_request/feedback_request.js
M	frappe/core/doctype/feedback_request/feedback_request_list.js
M	frappe/core/doctype/file/file_list.js
M	frappe/core/doctype/report/boilerplate/controller.js
M	frappe/core/doctype/role_permission_for_page_and_report/role_permission_for_page_and_report.js
M	frappe/core/doctype/system_settings/system_settings.js
M	frappe/core/page/data_import_tool/data_import_tool.js
M	frappe/core/page/desktop/desktop.js
M	frappe/core/page/permission_manager/permission_manager.js
M	frappe/core/page/user_permissions/user_permissions.js
M	frappe/core/report/permitted_documents_for_user/permitted_documents_for_user.js
M	frappe/custom/doctype/custom_field/custom_field.js
M	frappe/custom/doctype/customize_form/customize_form.js
M	frappe/desk/doctype/event/event.js
M	frappe/desk/doctype/kanban_board/kanban_board.js
M	frappe/desk/doctype/todo/todo.js
M	frappe/desk/page/activity/activity.js
M	frappe/desk/page/applications/applications.js
M	frappe/desk/page/backups/backups.js
M	frappe/desk/page/chat/chat.js
M	frappe/desk/page/modules/modules.js
M	frappe/desk/page/setup_wizard/setup_wizard.js
M	frappe/email/doctype/auto_email_report/auto_email_report.js
M	frappe/email/doctype/email_account/email_account.js
M	frappe/email/doctype/email_domain/email_domain.js
M	frappe/email/doctype/email_group/email_group.js
M	frappe/email/doctype/email_queue/email_queue_list.js
M	frappe/email/doctype/newsletter/newsletter.js
M	frappe/printing/page/print_format_builder/print_format_builder.js
M	frappe/public/js/frappe/form/grid.js
M	frappe/public/js/frappe/misc/utils.js
M	frappe/public/js/frappe/model/create_new.js
M	frappe/public/js/frappe/ui/filters/filters.js
M	frappe/public/js/frappe/ui/toolbar/search_utils.js
M	frappe/public/js/frappe/views/kanban/kanban_view.js
M	frappe/public/js/legacy/layout.js
M	frappe/public/js/legacy/print_table.js
R100	frappe/public/js/frappe/views/kanban/fluxify.min.js	frappe/public/js/lib/fluxify.min.js
M	frappe/templates/includes/contact.js
M	frappe/website/doctype/web_form/web_form.js
M	frappe/website/doctype/website_theme/website_theme.js
M	frappe/website/js/web_form.js
M	frappe/website/js/website.js
M	socketio.js

Rename validated to frappe.validated
M	frappe/custom/doctype/property_setter/property_setter.js
M	frappe/public/js/legacy/form.js

Update eslint
M	.eslintignore
M	.eslintrc

Fixed tab spacing
M	frappe/core/doctype/user/user.js
M	frappe/custom/doctype/customize_form/customize_form.js
M	frappe/public/js/frappe/db.js
M	frappe/public/js/frappe/desk.js
M	frappe/public/js/frappe/form/control.js
M	frappe/public/js/frappe/form/footer/timeline.js
M	frappe/public/js/frappe/form/footer/timeline_item.html
M	frappe/public/js/frappe/form/grid.js
M	frappe/public/js/frappe/form/layout.js
M	frappe/public/js/frappe/form/link_selector.js
M	frappe/public/js/frappe/form/print.js
M	frappe/public/js/frappe/form/save.js
M	frappe/public/js/frappe/form/script_manager.js
M	frappe/public/js/frappe/form/share.js
M	frappe/public/js/frappe/form/sidebar.js
M	frappe/public/js/frappe/misc/pretty_date.js
M	frappe/public/js/frappe/misc/user.js
M	frappe/public/js/frappe/misc/utils.js
M	frappe/public/js/frappe/model/create_new.js
M	frappe/public/js/frappe/model/model.js
M	frappe/public/js/frappe/roles_editor.js
M	frappe/public/js/frappe/ui/charts.js
M	frappe/public/js/frappe/ui/filters/filters.js
M	frappe/public/js/frappe/ui/messages.js
M	frappe/public/js/frappe/ui/page.js
M	frappe/public/js/frappe/ui/toolbar/search_utils.js
M	frappe/public/js/frappe/upload.js
M	frappe/public/js/frappe/views/calendar/calendar.js
M	frappe/public/js/frappe/views/communication.js
M	frappe/public/js/frappe/views/inbox/inbox_view.js
M	frappe/public/js/frappe/views/reports/grid_report.js
M	frappe/public/js/frappe/views/reports/query_report.js
M	frappe/public/js/frappe/views/reports/reportview.js
M	frappe/public/js/legacy/clientscriptAPI.js
M	frappe/public/js/legacy/dom.js
M	frappe/public/js/legacy/form.js
M	frappe/public/js/legacy/print_format.js

Add eslint files
A	.eslintignore
A	.eslintrc

Remove all implicit global variables
M	frappe/core/doctype/communication/communication.js
M	frappe/core/doctype/feedback_trigger/feedback_trigger.js
M	frappe/core/doctype/system_settings/system_settings.js
M	frappe/core/doctype/user/user.js
M	frappe/core/page/data_import_tool/data_import_tool.js
M	frappe/core/page/modules_setup/modules_setup.js
M	frappe/core/page/permission_manager/permission_manager.js
M	frappe/core/page/user_permissions/user_permissions.js
M	frappe/custom/doctype/customize_form/customize_form.js
M	frappe/custom/doctype/property_setter/property_setter.js
M	frappe/desk/doctype/todo/todo_list.js
M	frappe/desk/page/activity/activity.js
M	frappe/desk/page/chat/chat.js
M	frappe/email/doctype/auto_email_report/auto_email_report.js
M	frappe/email/doctype/email_alert/email_alert.js
M	frappe/email/doctype/newsletter/newsletter.js
M	frappe/printing/doctype/print_format/print_format.js
M	frappe/printing/page/print_format_builder/print_format_builder.js
M	frappe/public/js/frappe/assets.js
M	frappe/public/js/frappe/defaults.js
M	frappe/public/js/frappe/desk.js
M	frappe/public/js/frappe/dom.js
M	frappe/public/js/frappe/feedback.js
M	frappe/public/js/frappe/form/control.js
M	frappe/public/js/frappe/form/dashboard.js
M	frappe/public/js/frappe/form/footer/assign_to.js
M	frappe/public/js/frappe/form/footer/attachments.js
M	frappe/public/js/frappe/form/footer/timeline.js
M	frappe/public/js/frappe/form/form_viewers.js
M	frappe/public/js/frappe/form/formatters.js
M	frappe/public/js/frappe/form/grid.js
M	frappe/public/js/frappe/form/layout.js
M	frappe/public/js/frappe/form/link_selector.js
M	frappe/public/js/frappe/form/print.js
M	frappe/public/js/frappe/form/quick_entry.js
M	frappe/public/js/frappe/form/save.js
M	frappe/public/js/frappe/form/script_manager.js
M	frappe/public/js/frappe/form/share.js
M	frappe/public/js/frappe/form/sidebar.js
M	frappe/public/js/frappe/form/toolbar.js
M	frappe/public/js/frappe/form/workflow.js
M	frappe/public/js/frappe/list/list_renderer.js
M	frappe/public/js/frappe/list/list_sidebar.js
M	frappe/public/js/frappe/list/list_view.js
M	frappe/public/js/frappe/misc/common.js
M	frappe/public/js/frappe/misc/datetime.js
M	frappe/public/js/frappe/misc/number_format.js
M	frappe/public/js/frappe/misc/pretty_date.js
M	frappe/public/js/frappe/misc/tools.js
M	frappe/public/js/frappe/misc/user.js
M	frappe/public/js/frappe/misc/utils.js
M	frappe/public/js/frappe/model/create_new.js
M	frappe/public/js/frappe/model/meta.js
M	frappe/public/js/frappe/model/model.js
M	frappe/public/js/frappe/model/perm.js
M	frappe/public/js/frappe/model/workflow.js
M	frappe/public/js/frappe/request.js
M	frappe/public/js/frappe/roles_editor.js
M	frappe/public/js/frappe/router.js
M	frappe/public/js/frappe/socketio_client.js
M	frappe/public/js/frappe/toolbar.js
M	frappe/public/js/frappe/translate.js
M	frappe/public/js/frappe/ui/base_list.js
M	frappe/public/js/frappe/ui/charts.js
M	frappe/public/js/frappe/ui/field_group.js
M	frappe/public/js/frappe/ui/filters/filters.js
M	frappe/public/js/frappe/ui/like.js
M	frappe/public/js/frappe/ui/listing.js
M	frappe/public/js/frappe/ui/messages.js
M	frappe/public/js/frappe/ui/toolbar/about.js
M	frappe/public/js/frappe/ui/toolbar/awesome_bar.js
M	frappe/public/js/frappe/ui/toolbar/notifications.js
M	frappe/public/js/frappe/ui/toolbar/search.js
M	frappe/public/js/frappe/ui/toolbar/search_utils.js
M	frappe/public/js/frappe/ui/toolbar/toolbar.js
M	frappe/public/js/frappe/ui/tree.js
M	frappe/public/js/frappe/upload.js
M	frappe/public/js/frappe/views/calendar/calendar.js
M	frappe/public/js/frappe/views/communication.js
M	frappe/public/js/frappe/views/gantt/gantt_view.js
M	frappe/public/js/frappe/views/image/image_view.js
M	frappe/public/js/frappe/views/inbox/inbox_view.js
M	frappe/public/js/frappe/views/kanban/kanban_board.js
M	frappe/public/js/frappe/views/pageview.js
M	frappe/public/js/frappe/views/reports/grid_report.js
M	frappe/public/js/frappe/views/reports/query_report.js
M	frappe/public/js/frappe/views/reports/reportview.js
M	frappe/public/js/frappe/views/test_runner.js
M	frappe/public/js/frappe/views/treeview.js
M	frappe/public/js/legacy/clientscriptAPI.js
M	frappe/public/js/legacy/datatype.js
M	frappe/public/js/legacy/dom.js
M	frappe/public/js/legacy/form.js
M	frappe/public/js/legacy/handler.js
M	frappe/public/js/legacy/layout.js
M	frappe/public/js/legacy/print_format.js
M	frappe/public/js/legacy/print_table.js
M	frappe/templates/includes/contact.js
M	frappe/website/doctype/website_settings/website_settings.js

Password strength fix (#3419)
M	frappe/core/doctype/user/user.py
M	frappe/www/update-password.html

[translation] translation updates (#3409)
M	frappe/translations/am.csv
M	frappe/translations/ar.csv
M	frappe/translations/bg.csv
M	frappe/translations/bn.csv
M	frappe/translations/bs.csv
M	frappe/translations/ca.csv
M	frappe/translations/cs.csv
M	frappe/translations/da.csv
M	frappe/translations/de.csv
M	frappe/translations/el.csv
M	frappe/translations/es-PE.csv
M	frappe/translations/es.csv
M	frappe/translations/et.csv
M	frappe/translations/fa.csv
M	frappe/translations/fi.csv
M	frappe/translations/fr.csv
M	frappe/translations/gu.csv
M	frappe/translations/he.csv
M	frappe/translations/hi.csv
M	frappe/translations/hr.csv
M	frappe/translations/hu.csv
M	frappe/translations/id.csv
M	frappe/translations/is.csv
M	frappe/translations/it.csv
M	frappe/translations/ja.csv
M	frappe/translations/km.csv
M	frappe/translations/kn.csv
M	frappe/translations/ko.csv
M	frappe/translations/ku.csv
M	frappe/translations/lo.csv
M	frappe/translations/lt.csv
M	frappe/translations/lv.csv
M	frappe/translations/mk.csv
M	frappe/translations/ml.csv
M	frappe/translations/mr.csv
M	frappe/translations/ms.csv
M	frappe/translations/my.csv
M	frappe/translations/nl.csv
M	frappe/translations/no.csv
M	frappe/translations/pl.csv
M	frappe/translations/ps.csv
M	frappe/translations/pt-BR.csv
M	frappe/translations/pt.csv
M	frappe/translations/ro.csv
M	frappe/translations/ru.csv
M	frappe/translations/si.csv
M	frappe/translations/sk.csv
M	frappe/translations/sl.csv
M	frappe/translations/sq.csv
M	frappe/translations/sr.csv
M	frappe/translations/sv.csv
M	frappe/translations/ta.csv
M	frappe/translations/te.csv
M	frappe/translations/th.csv
M	frappe/translations/tr.csv
M	frappe/translations/uk.csv
M	frappe/translations/ur.csv
M	frappe/translations/vi.csv
M	frappe/translations/zh-TW.csv
M	frappe/translations/zh.csv

Fix fav button margin in RTL (#3393)
M	frappe/public/css/desk-rtl.css

[minor] changed the message field property reqd to 1 in Feedback Trigger (#3416)
M	frappe/core/doctype/feedback_trigger/feedback_trigger.json

[travis] Install node v7
M	.travis.yml

Cascade bootstrap css instead of replacing
M	frappe/website/doctype/website_theme/website_theme.py

Fix "Print Format Builder" translation  (#3403)
M	frappe/config/setup.py
M	frappe/core/doctype/feedback_trigger/feedback_trigger.json

Issue with ToDo WYSIWG area (#3374) (fixes frappe/erpnext#7773)
M	frappe/public/js/frappe/form/control.js

Replaced spaces with underscore in filename (#3386)
M	frappe/public/js/frappe/upload.js

Gantt milestones  (#3370)
M	frappe/public/build.json
A	frappe/public/css/gantt.css
M	frappe/public/js/frappe/views/gantt/gantt_view.js
A	frappe/public/less/gantt.less

Update hooks.md
M	frappe/docs/user/en/guides/basics/hooks.md

translations on communications.js
M	frappe/core/doctype/communication/communication.js

[translation] translation updates (#3367)
M	frappe/translations/am.csv
M	frappe/translations/ar.csv
M	frappe/translations/bg.csv
M	frappe/translations/bn.csv
M	frappe/translations/bs.csv
M	frappe/translations/ca.csv
M	frappe/translations/cs.csv
M	frappe/translations/da.csv
M	frappe/translations/de.csv
M	frappe/translations/el.csv
M	frappe/translations/es-CL.csv
M	frappe/translations/es-MX.csv
M	frappe/translations/es-PE.csv
M	frappe/translations/es.csv
M	frappe/translations/et.csv
M	frappe/translations/fa.csv
M	frappe/translations/fi.csv
M	frappe/translations/fr.csv
M	frappe/translations/gu.csv
M	frappe/translations/he.csv
M	frappe/translations/hi.csv
M	frappe/translations/hr.csv
M	frappe/translations/hu.csv
M	frappe/translations/id.csv
M	frappe/translations/is.csv
M	frappe/translations/it.csv
M	frappe/translations/ja.csv
M	frappe/translations/km.csv
M	frappe/translations/kn.csv
M	frappe/translations/ko.csv
M	frappe/translations/ku.csv
M	frappe/translations/lo.csv
M	frappe/translations/lt.csv
M	frappe/translations/lv.csv
M	frappe/translations/mk.csv
M	frappe/translations/ml.csv
M	frappe/translations/mr.csv
M	frappe/translations/ms.csv
M	frappe/translations/my.csv
M	frappe/translations/nl.csv
M	frappe/translations/no.csv
M	frappe/translations/pl.csv
M	frappe/translations/ps.csv
M	frappe/translations/pt-BR.csv
M	frappe/translations/pt.csv
M	frappe/translations/ro.csv
M	frappe/translations/ru.csv
M	frappe/translations/si.csv
M	frappe/translations/sk.csv
M	frappe/translations/sl.csv
M	frappe/translations/sq.csv
M	frappe/translations/sr.csv
M	frappe/translations/sv.csv
M	frappe/translations/ta.csv
M	frappe/translations/te.csv
M	frappe/translations/th.csv
M	frappe/translations/tr.csv
M	frappe/translations/uk.csv
M	frappe/translations/ur.csv
M	frappe/translations/vi.csv
M	frappe/translations/zh-TW.csv
M	frappe/translations/zh.csv

Fixed issue #frappe WN-SUP25323 for password strength error (#3380)
M	frappe/utils/password_strength.py

superficial fix for charts site (#3373)
M	frappe/public/js/frappe/form/control.js

[translation] translation updates (#3343)
M	frappe/translations/da.csv
M	frappe/translations/fr.csv
M	frappe/translations/hu.csv
M	frappe/translations/lv.csv
M	frappe/translations/pt-BR.csv
M	frappe/translations/pt.csv

Add package.json (#3364)
A	package.json
```