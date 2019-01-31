
> kernel/power/qos.c

```c
void pm_qos_update_request(struct pm_qos_request *req, s32 new_value);
static void __pm_qos_update_request(struct pm_qos_request *req, s32 new_value);
int pm_qos(read_req_value();
#define pm_qos_add_request(arg...);
void pm_qos_add_request_trace(...);