---
title: Sort Multiple Checkbox Filter
page_title: Sort Multiple Checkbox Filter | Kendo UI Grid
description: "Learn how to sort the Kendo UI multiple checkbox filter while using the Kendo UI Grid widget."
slug: howto_sort_multiple_checkbox_filter_grid
---

# Sort Multiple Checkbox Filter

The example below demonstrates how to sort the Kendo UI multiple checkbox filter.

###### Example

```html

	<div id="client"></div>
      <script>
        $(document).ready(function() {
          var telerikWebServiceBase = "http://demos.telerik.com/kendo-ui/service/";
          $("#client").kendoGrid({
            dataSource: {
              transport: {
                read:  {
                  url: telerikWebServiceBase + "/Products",
                  dataType: "jsonp"
                },
                update: {
                  url: telerikWebServiceBase + "/Products/Update",
                  dataType: "jsonp"
                },
                destroy: {
                  url: telerikWebServiceBase + "/Products/Destroy",
                  dataType: "jsonp"
                },
                create: {
                  url: telerikWebServiceBase + "/Products/Create",
                  dataType: "jsonp"
                },
                parameterMap: function(options, operation) {
                  if (operation !== "read" && options.models) {
                    return {models: kendo.stringify(options.models)};
                  }
                }
              },
              batch: true,
              pageSize: 20,
              schema: {
                model: {
                  id: "ProductID",
                  fields: {
                    ProductID: { editable: false, nullable: true },
                    ProductName: { validation: { required: true } },
                    UnitPrice: { type: "number", validation: { required: true, min: 1} },
                    Discontinued: { type: "boolean" },
                    UnitsInStock: { type: "number", validation: { min: 0, required: true } }
                  }
                }
              }
            },
            filterMenuInit: function(e) {
              if (e.field === "UnitPrice" || e.field === "UnitsInStock") {
                var filterMultiCheck = this.thead.find("[data-field=" + e.field + "]").data("kendoFilterMultiCheck")
                filterMultiCheck.container.empty();
                filterMultiCheck.checkSource.sort({field: e.field, dir: "asc"});

                filterMultiCheck.checkSource.data(filterMultiCheck.checkSource.view().toJSON());
                filterMultiCheck.createCheckBoxes();
              }
            },
            filterable: true,
            pageable: true,
            height: 550,
            toolbar: ["create", "save", "cancel"],
            columns: [
              { field: "ProductName", filterable: { multi: true } },
              { field: "UnitPrice", title: "Unit Price", format: "{0:c}", width: 120, filterable: { multi: true } },
              { field: "UnitsInStock", title: "Units In Stock", width: 120, filterable: { multi: true } },
              { field: "Discontinued", width: 120, filterable: { multi: true, dataSource: [{ Discontinued: true }, { Discontinued: false }]} },
              { command: "destroy", title: "&nbsp;", width: 150}],
            editable: true
          });
        });
      </script>
```

## See Also

Other articles on Kendo UI Grid and how-to examples:

* [JavaScript API Reference](/api/javascript/ui/grid)
* [How to Add Cascading DropDownList Editors]({% slug howto_add_cascading_dropdown_list_editors_grid %})
* [How to Add Tooltip to Grid Cells]({% slug howto_add_tooltipto_grid_cell_record_grid %})
* [How to Copy Data from Excel]({% slug howto_copy_datafrom_excel_grid %})
* [How to Create Checkbox Filter Menu]({% slug howto_create_checkbox_filter_menu_grid %})
* [How to Customize Rows and Cells Based on Data Item Values]({% slug howto_customize_rowsand_cells_basedon_dataitem_values_grid %})
* [How to Drag and Drop Rows between Grids]({% slug howto_dragand_drop_rows_between_twogrids_grid %})
* [How to Enable ForeignKey Column Sorting by Text]({% slug howto_enable_foreignkey_sotringby_text_grid %})
* [How to Filter Array Columns Using MultiSelect]({% slug howto_filetr_array_columns_using_multiselect_grid %})
* [How to Filter Grid as You Type]({% slug howto_filter_gridas_you_type_grid %})
* [How to Implement Stable Sort in Chrome]({% slug howto_implement_stable_sortin_chrome_grid %})
* [How to Initialize Data Attribute with Detail Template]({% slug howto_initialize_data_attributewith_detail_template_grid %})
* [How to Load and Append More Records While Scrolling Down]({% slug howto_loadand_append_morerecords_while_scrollingdown_grid %})
* [How to Perform CRUD Operations with Local Storage Data]({% slug howto_perform_crud_operationswith_local_storage_data_grid %})
* [How to Persist Collapsed State of Grouped Records]({% slug howto_persist_collapsed_stateof_grouped_records_grid %})
* [How to Persist Expanded Rows after Refresh]({% slug howto_persist_expanded_rows_afetrrefresh_grid %})
* [How to Preserve Grid State in a Cookie]({% slug howto_preserve_gridstate_inacookie_grid %})
* [How to Set Cell Color Based on ForeignKey Values]({% slug howto_set_cell_color_basedon_foreignkey_values_grid %})
* [How to Show Tooltip for Column Records]({% slug howto_show_tooltipfor_column_records_grid %})
* [How to Update Toolbar Content Using MVVM Binding]({% slug howto_update_toolbar_content_using_mvvmbinding_grid %})
* [How to Use Checkboxes inside Column Menus]({% slug howto_use_checkboxes_inside_column_menu_grid %})
* [How to Use Draggable Elements with Multiselection Enabled]({% slug howto_use_draggable_elements_multiselection_enabled_grid %})
* [How to Use Grid in Kendo UI SPA Application]({% slug howto_use_gridin_kendouispa_app_grid %})
* [How to Use MultiSelect for Column Filtering]({% slug howto_use_multiselect_forcolumn_filtering_grid %})
* [How to Use Nested Chart]({% slug howto_use_nested_charts_grid %})
* [How to Use Nested Model Properties]({% slug howto_use_nested_model_properties_grid %})
* [How to Use WebAPI with Server-Side Operations]({% slug howto_use_webapi_withserverside_operations_grid %})
