---
title: Edit Using ContextMenu
page_title: Edit Using ContextMenu | Kendo UI Scheduler Widget
description: "Learn how to edit the kendo UI Scheduler widget event using Kendo UI ContextMenu."
slug: howto_edit_using_contectmenu_angularjs_scheduler
---

# Edit Using ContextMenu

The example below demonstrates how to edit the Scheduler widget event using Kendo UI ContextMenu in AngularJS.

###### Example

```html
     <div id="example" ng-app="KendoDemos">
      <div ng-controller="MyCtrl">
        <div kendo-scheduler="scheduler" k-options="schedulerOptions"></div>


        <ul kendo-context-menu="contextMenu"
            k-filter="'.k-event, .k-scheduler-table'"
            k-show-on="'click'"
            k-on-select="onContextMenuSelect(kendoEvent);"
            k-on-open="onContextMenuOpen(kendoEvent);">
        </ul>

      </div>
      <style>
        .custom-event {
          text-shadow: 0 1px 1px #000;
        }
        .custom-all-day-event {
          text-align: center;
          text-transform: uppercase
        }
      </style>
    </div>

    <script>
      angular.module("KendoDemos", [ "kendo.directives" ])
        .controller("MyCtrl", function($scope){

        $scope.onContextMenuOpen = function(e) {
          var menu = $scope.contextMenu;
          var text = $(e.target).hasClass("k-event") ? "Edit event" : "Add Event";

          menu.remove(".myClass");
          menu.append([{text: text, cssClass: "myClass" }]);
        };

        $scope.onContextMenuSelect = function (e) {
          var scheduler = $scope.scheduler;
          var state = $scope.selectState;

          if (state.events.length) {
            scheduler.editEvent(state.events[0]);
          } else {
            scheduler.addEvent({
              start: state.start,
              end: state.end
            });
          }
        };

        $scope.schedulerOptions = {
          date: new Date("2013/6/13"),
          startTime: new Date("2013/6/13 07:00 AM"),
          height: 600,
					views: [
            "day",
            { type: "workWeek", selected: true },
            "week",
            "month",
          ],
          selectable: true,
          change: function(e) {
            $scope.selectState = e;
          },
          eventTemplate: "<span class='custom-event'>{{dataItem.title}}</span>",
          allDayEventTemplate: "<div class='custom-all-day-event'>{{dataItem.title}}</div>",
          timezone: "Etc/UTC",
          dataSource: {
            batch: true,
            transport: {
              read: {
                url: "http://demos.telerik.com/kendo-ui/service/tasks",
                dataType: "jsonp"
              },
              update: {
                url: "http://demos.telerik.com/kendo-ui/service/tasks/update",
                dataType: "jsonp"
              },
              create: {
                url: "http://demos.telerik.com/kendo-ui/service/tasks/create",
                dataType: "jsonp"
              },
              destroy: {
                url: "http://demos.telerik.com/kendo-ui/service/tasks/destroy",
                dataType: "jsonp"
              },
              parameterMap: function(options, operation) {
                if (operation !== "read" && options.models) {
                  return {models: kendo.stringify(options.models)};
                }
              }
            },
            schema: {
              model: {
                id: "taskId",
                fields: {
                  taskId: { from: "TaskID", type: "number" },
                  title: { from: "Title", defaultValue: "No title", validation: { required: true } },
                  start: { type: "date", from: "Start" },
                  end: { type: "date", from: "End" },
                  startTimezone: { from: "StartTimezone" },
                  endTimezone: { from: "EndTimezone" },
                  description: { from: "Description" },
                  recurrenceId: { from: "RecurrenceID" },
                  recurrenceRule: { from: "RecurrenceRule" },
                  recurrenceException: { from: "RecurrenceException" },
                  ownerId: { from: "OwnerID", defaultValue: 1 },
                  isAllDay: { type: "boolean", from: "IsAllDay" }
                }
              }
            },
            filter: {
              logic: "or",
              filters: [
                { field: "ownerId", operator: "eq", value: 1 },
                { field: "ownerId", operator: "eq", value: 2 }
              ]
            }
          },
          resources: [
            {
              field: "ownerId",
              title: "Owner",
              dataSource: [
                { text: "Alex", value: 1, color: "#f8a398" },
                { text: "Bob", value: 2, color: "#51a0ed" },
                { text: "Charlie", value: 3, color: "#56ca85" }
              ]
            }
          ]
        };
      });
    </script>
```


## See Also 

Other how-to examples on Kendo UI Scheduler in AngularJS:

* [How to Create and Set `ObservableArray` Events]({% slug howto_createand_set_observablearray_events_angularjs_scheduler %})
* [How to Customize Edit and Event Templates]({% slug howto_createand_set_observablearray_events_angularjs_scheduler %})
* [How to Set Initial Data Manually]({% slug howto_set_intial_data_manually_angularjs_scheduler %})
* [How to Show Тooltip on `hover`]({% slug howto_show_tooltipon_hover_angularjs_scheduler %})
* [How to Wrap Scheduler in Custom Directives]({% slug howto_wrap_schedulerin_custom_directives_angularjs_scheduler %})

Other articles and how-to examples on Kendo UI Scheduler:

* [JavaScript API Reference](/api/javascript/ui/scheduler)
* [How to Add Controls to Custom Editor]({% slug howto_add_controlsto_custom_event_editor_scheduler %})
* [How to Add Events Programatically]({% slug howto_add_events_programatically_scheduler %})
* [How to Calculate Scheduler Height Dynamically]({% slug howto_calculate_scheduler_height_dunamically_scheduler %})
* [How to Calculate Scheduler Height Dynamically on Mobile]({% slug howto_calculate_scheduler_height_dunamically_onmobile_scheduler %})
* [How to Clone Events on `Ctrl`+`move`]({% slug howto_clone_eventson_ctrlplus_move_scheduler %})
* [How to Create Custom Views Inheriting Built-In Views]({% slug howto_create_custom_view_inheriting_builtinview_scheduler %})
* [How to Create Custom `month` View with Event Count in **Show More** Button]({% slug howto_create_custom_monthview_eventcount_showmore_button_scheduler %})
* [How to Create Custom Restrictions]({% slug howto_create_custom_restrivtions_scheduler %})
* [How to Customize Edit and Events Templates]({% slug howto_customize_editand_event_templates_scheduler %})
* [How to Create External Editor Form]({% slug howto_create_external_editor_form_scheduler %})
* [How to Edit Records on `touchend`]({% slug howto_edit_records_using_touchendonmobile_scheduler %})
* [How to Edit Using ContextMenu]({% slug howto_edit_using_kendouicontextmenu_scheduler %})
* [How to Expand Scheduler to 100% Width and Height]({% slug howto_expand_scheduler_to100percent_widthandheight_scheduler %})
* [How to Filter Events by Resource Using MultiSelect]({% slug howto_filter_eventsby_resourceusing_multiselect_scheduler %})
* [How to Get `next` Occurance]({% slug howto_getthe_next_occurance_scheduler %})
* [How to Get Reference to the Built-In Validator]({% slug howto_get_referencetothe_builtin_validator_scheduler %})
* [How to Hide Edit Buttons]({% slug howto_hidethe_editbutons_scheduler %})
* [How to Implement Custom Editing in `agenda` View]({% slug howto_implement_custom_editing_inagenda_view_scheduler %})
* [How to Nest Editors inside Event Templates]({% slug howto_nest_editorsinside_event_templates_scheduler %})
* [How to Use Custom Event Template with Specific Background Color]({% slug howto_use_custom_event_templatewith_specific_background_color_scheduler %})

For additional runnable examples on Kendo UI Scheduler, browse the [Scheduler **How To** documentation folder](http://docs.telerik.com/kendo-ui/web/scheduler/how-to).