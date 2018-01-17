# Lab: Public APIs for Libs

## Scenario

## Instructions
1. Create a new interface for an `EventLog` data model in the **data-models** lib.
```
export interface EventLog {
  id: number;
  message: string;
  userId: number;
  resourceType: string;
  resourceId: number;
}
```
2. Export the `EventLog` in the **data-models** `index.ts` file to make it "public".
1. Add the `HttpClientModule` to the **logs-backend** module.
1. Use the Angular CLI schematic for generating a new service to create a new service named **log** to the **logs-backend** lib with the `-a` option. Include the `module` option to tell the CLI schematic to include the service in the `providers` NgModule metadata (`--module=logs-backend.module.ts`).
1. Set up the `LogService` logic:
```
export class LogService {
  private _rootUrl = '';
  constructor(@Optional() private apiConfig: ApiConfig, private http: HttpClient) {
    if (apiConfig) {
      this._rootUrl = apiConfig.rootUrl;
    }
  }
  logs(): Observable<EventLog[]> {
    return this.http.get<EventLog[]>(`${this._rootUrl}/api/eventlogs`);
  }
}
```
6. The `ApiConfig` type is not public (you should see the tslint error). Make it public by adding an export of it to the **backlog** lib `index.ts` file. Back in the `LogService` make sure the import path for `ApiConfig` is set to `@tuskdesk-suite/backend`.
1. Add an export for the `LogService` to the **logs-backend** `index.ts` file to make it public.
1. Refactor the `LogsListComponent` to inject the `LogService` (use the npm scope short path for the import) and use it to get logs from the `logs` method. You can `subscribe` to that and set the `logs` class field with the data, or you can make use of the `async` pipe.

## Next Lab
Go to []()