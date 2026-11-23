# Reference
## Health
<details><summary><code>client.health.<a href="/src/api/resources/health/client/Client.ts">check</a>() -> Record&lt;string, string&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Liveness probe. evcloud holds no state, so live means ready.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.health.check();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Cdrs
<details><summary><code>client.cpo.cdrs.<a href="/src/api/resources/cpo/resources/cdrs/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.CdrOut, Evcloud.CdrPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Charge detail records produced from charger traffic, newest start first, optionally within a time window.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.cdrs.list({
    charge_point_id: "CP-AMS-001",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.cdrs.list({
    charge_point_id: "CP-AMS-001",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListCdrsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CdrsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.cdrs.<a href="/src/api/resources/cpo/resources/cdrs/client/Client.ts">get</a>({ ...params }) -> Evcloud.CdrOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One CDR by OCPI id. If two parties use the same id, pass ``country_code`` and ``party_id`` (409 otherwise).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.cdrs.get({
    cdr_id: "CDR-2026-09-30-0001",
    country_code: "NL",
    party_id: "OCP"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetCdrsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CdrsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo ChargePoints
<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.ChargePointOut, Evcloud.ChargePointPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your chargers, sorted by OCPP identity. Online state, heartbeat and firmware come from the chargers themselves.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.chargePoints.list({
    is_online: true,
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.chargePoints.list({
    is_online: true,
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">create</a>({ ...params }) -> Evcloud.ChargePointCreatedOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a charger. It starts offline. The gateway refuses its connection until the charger is registered with the gateway; ``gateway_registered`` says whether it already is. 409 if the OCPP identity is taken.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.chargePoints.create({
    charge_point_id: "CP-AMS-001",
    ocpp_version: "ocpp2.0.1",
    charge_point_vendor: "ABB",
    charge_point_model: "Terra AC W22",
    location_id: 12,
    max_power_kw: 22,
    connector_count: 2,
    is_roaming: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ChargePointCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">get</a>({ ...params }) -> Evcloud.ChargePointOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One charger by its OCPP identity.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.chargePoints.get({
    charge_point_id: "CP-AMS-001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the charger with its EVSEs and connectors. Refused with 409 while charging sessions reference it, because that would erase their history.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.chargePoints.delete({
    charge_point_id: "CP-AMS-001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.DeleteChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">update</a>({ ...params }) -> Evcloud.ChargePointOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes only the fields sent; send null to clear a field. Send ``expected_revision`` to have the update refused with 409 if the charger changed since you read it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.chargePoints.update({
    charge_point_id: "CP-AMS-001",
    location_id: 13,
    expected_revision: 1
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ChargePointUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">listCdrs</a>({ ...params }) -> core.Page&lt;Evcloud.CdrOut, Evcloud.CdrPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

CDRs of sessions on the charger, newest start first, optionally within a time window. 404 if the charger does not exist.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.chargePoints.listCdrs({
    charge_point_id: "CP-AMS-001",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.chargePoints.listCdrs({
    charge_point_id: "CP-AMS-001",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListCdrsChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">listConnectors</a>({ ...params }) -> core.Page&lt;Evcloud.CpoConnectorOut, Evcloud.ConnectorPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The charger's connectors. 404 if the charger does not exist.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.chargePoints.listConnectors({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.chargePoints.listConnectors({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListConnectorsChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">listEvses</a>({ ...params }) -> core.Page&lt;Evcloud.CpoEvseOut, Evcloud.EvsePage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The charger's EVSEs. 404 if the charger does not exist.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.chargePoints.listEvses({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.chargePoints.listEvses({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListEvsesChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.chargePoints.<a href="/src/api/resources/cpo/resources/chargePoints/client/Client.ts">listSessions</a>({ ...params }) -> core.Page&lt;Evcloud.SessionOut, Evcloud.SessionPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Charging sessions on the charger, newest start first, optionally within a time window. 404 if the charger does not exist.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.chargePoints.listSessions({
    charge_point_id: "CP-AMS-001",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.chargePoints.listSessions({
    charge_point_id: "CP-AMS-001",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListSessionsChargePointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargePointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Connectors
<details><summary><code>client.cpo.connectors.<a href="/src/api/resources/cpo/resources/connectors/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.CpoConnectorOut, Evcloud.ConnectorPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your connectors, newest first, optionally of one EVSE or charger.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.connectors.list({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.connectors.list({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListConnectorsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConnectorsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.connectors.<a href="/src/api/resources/cpo/resources/connectors/client/Client.ts">create</a>({ ...params }) -> Evcloud.CpoConnectorOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds a connector to one of your EVSEs; the charger, OCPI EVSE uid and OCPP version are copied from the EVSE. 409 if the EVSE is partner data.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.connectors.create({
    evse_db_id: 101,
    connector_id: 1,
    evse_type_connector_id: 1,
    ocpi_connector_id: "1",
    standard: "IEC_62196_T2",
    format: "SOCKET",
    power_type: "AC_3_PHASE",
    max_voltage: 400,
    max_amperage: 32,
    max_electric_power: 22000
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ConnectorCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConnectorsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.connectors.<a href="/src/api/resources/cpo/resources/connectors/client/Client.ts">get</a>({ ...params }) -> Evcloud.CpoConnectorOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One connector by its ``id``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.connectors.get({
    connector_db_id: 201
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetConnectorsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConnectorsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.connectors.<a href="/src/api/resources/cpo/resources/connectors/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the connector; charging history keeps its sessions. Connectors of partner EVSEs are read-only (409).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.connectors.delete({
    connector_db_id: 201
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.DeleteConnectorsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConnectorsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.connectors.<a href="/src/api/resources/cpo/resources/connectors/client/Client.ts">update</a>({ ...params }) -> Evcloud.CpoConnectorOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes only the fields sent; send null to clear a field. Connectors of partner EVSEs are read-only (409).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.connectors.update({
    connector_db_id: 201,
    max_electric_power: 11000
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ConnectorUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConnectorsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Evses
<details><summary><code>client.cpo.evses.<a href="/src/api/resources/cpo/resources/evses/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.CpoEvseOut, Evcloud.EvsePage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your live EVSEs, newest first, optionally of one location or charger.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.evses.list({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.evses.list({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListEvsesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EvsesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.evses.<a href="/src/api/resources/cpo/resources/evses/client/Client.ts">create</a>({ ...params }) -> Evcloud.CpoEvseOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds an EVSE to one of your chargers. Set ``location_id`` and ``evse_uid`` so its connectors can be priced and roaming commands reach it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.evses.create({
    charge_point_id: "CP-AMS-001",
    evse_type_id: 1,
    evse_uid: "NL*OCP*E1001*1",
    evse_id: "NL*OCP*E1001*1",
    location_id: "LOC-AMS-01",
    capabilities: ["RFID_READER", "REMOTE_START_STOP_CAPABLE"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.EvseCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EvsesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.evses.<a href="/src/api/resources/cpo/resources/evses/client/Client.ts">get</a>({ ...params }) -> Evcloud.CpoEvseOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One live EVSE by its ``id``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.evses.get({
    id: 101
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetEvsesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EvsesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.evses.<a href="/src/api/resources/cpo/resources/evses/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the EVSE from reads and ends the tariff links on its connectors. Its id stays reserved.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.evses.delete({
    id: 101
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.DeleteEvsesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EvsesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.evses.<a href="/src/api/resources/cpo/resources/evses/client/Client.ts">update</a>({ ...params }) -> Evcloud.CpoEvseOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes only the fields sent; send null to clear a field. Guard it with ``expected_revision`` to avoid overwriting someone else's change.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.evses.update({
    id: 101,
    floor_level: "-1",
    expected_revision: 1
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.EvseUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EvsesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Health
<details><summary><code>client.cpo.health.<a href="/src/api/resources/cpo/resources/health/client/Client.ts">get</a>() -> Evcloud.HealthOk</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Answers ``ok`` when the CPO service is up; 502 or 504 when it is not.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.health.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Locations
<details><summary><code>client.cpo.locations.<a href="/src/api/resources/cpo/resources/locations/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.LocationOut, Evcloud.LocationPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your locations and those received from roaming partners, most recently changed first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.locations.list({
    publish: true,
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.locations.list({
    publish: true,
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.locations.<a href="/src/api/resources/cpo/resources/locations/client/Client.ts">create</a>({ ...params }) -> Evcloud.LocationOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a location under your OCPI party. A location id is never reused, even after the location is deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.locations.create({
    location_id: "LOC-AMS-01",
    name: "Amsterdam depot",
    address: "Stationsplein 1",
    city: "Amsterdam",
    postal_code: "1012AB",
    country: "NLD",
    coordinates: {
        latitude: "52.37310",
        longitude: "4.88970"
    },
    time_zone: "Europe/Amsterdam",
    parking_type: "PARKING_LOT",
    facilities: ["TRAIN_STATION"],
    publish: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.LocationCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.locations.<a href="/src/api/resources/cpo/resources/locations/client/Client.ts">get</a>({ ...params }) -> Evcloud.LocationOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One location by OCPI id. If two parties use the same id, pass ``country_code`` and ``party_id`` (409 otherwise).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.locations.get({
    location_id: "LOC-AMS-01"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.locations.<a href="/src/api/resources/cpo/resources/locations/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes one of your locations from reads; its OCPI id stays reserved. Partner locations are read-only (409).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.locations.delete({
    location_id: "LOC-AMS-01"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.DeleteLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.locations.<a href="/src/api/resources/cpo/resources/locations/client/Client.ts">update</a>({ ...params }) -> Evcloud.LocationOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes only the fields sent; send null to clear a field. Guard it with ``expected_revision`` to avoid overwriting someone else's change. Partner locations are read-only (409).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.locations.update({
    location_id: "LOC-AMS-01",
    publish: false,
    expected_revision: 1
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.LocationPatch` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Sessions
<details><summary><code>client.cpo.sessions.<a href="/src/api/resources/cpo/resources/sessions/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.SessionOut, Evcloud.SessionPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Charging sessions recorded from charger traffic, newest start first, optionally within a time window.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.sessions.list({
    status: "COMPLETED",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.sessions.list({
    status: "COMPLETED",
    date_from: "2026-09-30T00:00:00Z",
    date_to: "2026-10-01T00:00:00Z",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.sessions.<a href="/src/api/resources/cpo/resources/sessions/client/Client.ts">get</a>({ ...params }) -> Evcloud.SessionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One session by OCPI id. If two parties use the same id, pass ``country_code`` and ``party_id`` (409 otherwise).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.sessions.get({
    session_id: "S-2026-09-30-0001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.sessions.<a href="/src/api/resources/cpo/resources/sessions/client/Client.ts">getCdr</a>({ ...params }) -> Evcloud.CdrOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The CDR that billed the session. 404 if the session does not exist or has no CDR yet.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.sessions.getCdr({
    session_id: "S-2026-09-30-0001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetCdrSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cpo Tariffs
<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">listAssignments</a>({ ...params }) -> core.Page&lt;Evcloud.TariffAssignmentOut, Evcloud.TariffAssignmentPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Which tariff each of your chargers uses, newest first. A charger uses one tariff at a time. Ended assignments are history, returned with ``include_deleted``. ``date_from`` and ``date_to`` filter on when the charger started using the tariff.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.tariffs.listAssignments({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.tariffs.listAssignments({
    charge_point_id: "CP-AMS-001",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListAssignmentsTariffsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.TariffOut, Evcloud.TariffPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your live tariffs, most recently changed first. ``date_from`` and ``date_to`` filter on ``last_updated``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.cpo.tariffs.list({
    currency: "EUR",
    limit: 50,
    offset: 0
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.cpo.tariffs.list({
    currency: "EUR",
    limit: 50,
    offset: 0
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.ListTariffsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">create</a>({ ...params }) -> Evcloud.TariffOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a tariff under your OCPI party. The id of a deleted tariff brings that tariff back as the body describes it. ``is_roaming`` marks it for roaming partners. Assign it to chargers with ``POST /cpo/tariffs/{tariff_id}/assign``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.tariffs.create({
    tariff_id: "TARIFF-AC-STD",
    country_code: "NL",
    party_id: "OCP",
    currency: "EUR",
    type: "REGULAR",
    elements: [{
            price_components: [{
                    type: "ENERGY",
                    price: "0.35",
                    step_size: 1
                }]
        }],
    ocpi_version: "2.3.0"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.TariffCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">get</a>({ ...params }) -> Evcloud.TariffOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One tariff by OCPI id. If two parties use the same id, pass ``country_code`` and ``party_id`` (409 otherwise).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.tariffs.get({
    tariff_id: "TARIFF-AC-STD"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.GetTariffsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the tariff from reads; the chargers that use it stop using it. Sessions already started keep their price.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.tariffs.delete({
    tariff_id: "TARIFF-AC-STD"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.DeleteTariffsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">update</a>({ ...params }) -> Evcloud.TariffOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes only the fields sent; send null to clear an optional field. ``currency``, ``elements``, ``p2p_preset`` and ``is_roaming`` cannot be cleared. ``expected_revision`` refuses a lost update with 409. Sessions already started keep their price.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.tariffs.update({
    tariff_id: "TARIFF-AC-STD",
    elements: [{
            price_components: [{
                    type: "ENERGY",
                    price: "0.39",
                    step_size: 1
                }]
        }],
    expected_revision: 1
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.TariffPatch` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">assign</a>({ ...params }) -> Evcloud.TariffAssignmentOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Makes one charger use this tariff; a charger uses one tariff at a time. A charger already on this tariff gets its assignment back unchanged. A charger on another tariff is refused with 409 unless ``replace`` is true, which ends that assignment. Sessions already started keep their price.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.tariffs.assign({
    tariff_id: "TARIFF-AC-STD",
    charge_point_id: "CP-AMS-001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.TariffAssignmentCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cpo.tariffs.<a href="/src/api/resources/cpo/resources/tariffs/client/Client.ts">unassign</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Ends the charger's assignment to this tariff; it stays as history. 404 when the charger does not use this tariff. Sessions already started keep their price.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.cpo.tariffs.unassign({
    tariff_id: "TARIFF-AC-STD",
    charge_point_id: "CP-AMS-001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.cpo.TariffUnassignment` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Health
<details><summary><code>client.emsp.health.<a href="/src/api/resources/emsp/resources/health/client/Client.ts">get</a>() -> Evcloud.HealthOk</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Answers ``{"status": "ok"}`` when the eMSP gateway is reachable.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.health.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Locations
<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.EmspGatewaySchemaLocationsLocationOut, Evcloud.EmspGatewaySchemaLocationsLocationPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your own OCPP chargers and roaming CPOs' locations, filtered by area, text, CPO, connector, power, facilities and parking type, optionally scoped to a network or a token group's networks. Each row carries a stable ``uid`` and its ``source`` (``OWN_OCPP`` or ``PARTNER_OCPI``).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.locations.list({
    limit: 50,
    lat: 52.37,
    lon: 4.89,
    radius_km: 5,
    availability: true,
    min_power: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.locations.list({
    limit: 50,
    lat: 52.37,
    lon: 4.89,
    radius_km: 5,
    availability: true,
    min_power: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">checkAvailability</a>({ ...params }) -> Evcloud.AvailabilityPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Free and total EVSEs per location. Unknown or out-of-scope ids are left out.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.checkAvailability({
    location_ids: ["LOC-AMS-001", "LOC-AMS-002"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.AvailabilityRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">cluster</a>({ ...params }) -> Evcloud.ClusterPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deprecated: use ``GET /emsp/locations/map``. Kept for one minor version. Groups locations into grid cells sized for the zoom level. A cell lists its location ids when it holds 20 or fewer.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.cluster({
    zoom_level: 7,
    bounding_box: "3.3,50.7,7.2,53.6"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ClusterLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">listFacilities</a>({ ...params }) -> Evcloud.FacilityPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Each OCPI facility present, with how many locations have it, most common first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.listFacilities({
    network_id: 21
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListFacilitiesLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">map</a>({ ...params }) -> Evcloud.MapPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pins (up to 500 location summaries) when ``zoom`` >= 13 or the box holds 500 locations or fewer; otherwise clusters on web-mercator tiles. ``tile_versions`` change when a tile's content changes. Answers are cached for a few seconds per workspace and query.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.map({
    bbox: "4.7,52.2,5.0,52.5",
    zoom: 11,
    available_only: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.MapLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">search</a>({ ...params }) -> Evcloud.LocationList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Text search on name, address and city (``q``), EVSE id lookup (``evse_id``, as printed on the QR code; ``*`` and case are ignored), or both. Nearest first when ``lat`` and ``lon`` are given. Returns at most ``limit`` matches with no next page: refine the query to narrow it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.search({
    evse_id: "NL*ABC*E1001*1",
    lat: 52.37,
    lon: 4.89
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.SearchLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">route</a>({ ...params }) -> Evcloud.LocationList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Locations within ``buffer_km`` of an encoded polyline (Google format, precision 5), in order along the route. Same filters as the map. Returns at most ``limit`` locations with no next page: shorten the route or ``buffer_km`` to narrow it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.route({
    polyline: "_p~iF~ps|U_ulLnnqC_mqNvxq`@",
    buffer_km: 2,
    min_power: 50
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.RouteLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">batch</a>({ ...params }) -> Evcloud.BatchResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Up to 500 locations by OCPI key or by ``uid`` (one of the two). Keys or uids that are unknown or out of scope come back in ``missing``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.batch({
    keys: [{
            country_code: "NL",
            party_id: "ABC",
            location_id: "LOC-AMS-001"
        }, {
            country_code: "NL",
            party_id: "ABC",
            location_id: "LOC-GONE"
        }]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.BatchRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">getByUid</a>({ ...params }) -> Evcloud.LocationDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One location with its EVSEs, connectors and tariff summary, by its stable ``uid``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.getByUid({
    uid: "3f2b8c1d-6e4a-4b7f-9c2d-8a1e5f0b7c34"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetByUidLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.locations.<a href="/src/api/resources/emsp/resources/locations/client/Client.ts">get</a>({ ...params }) -> Evcloud.LocationDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One own or partner location with its EVSEs, connectors and tariff summary, addressed by the CPO's country code and party id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.locations.get({
    location_id: "LOC-AMS-001",
    country_code: "NL",
    party_id: "ABC"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetLocationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LocationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Networks
<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.NetworkResponse, Evcloud.NetworkPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your base networks and the sub-networks that slice them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.networks.list({
    limit: 50,
    network_type: "TENANT"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.networks.list({
    limit: 50,
    network_type: "TENANT"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">create</a>({ ...params }) -> Evcloud.NetworkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A named slice of one of your base networks: some of its CPOs, optionally filtered by country, power, parking and facilities.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.create({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    name: "Fleet fast chargers",
    parent_network_id: 20,
    cpo_ids: ["NL*ABC", "BE*XYZ"],
    description: "DC sites only",
    countries: ["NLD", "BEL"],
    power_types: ["DC"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.NetworkCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">createBase</a>({ ...params }) -> Evcloud.NetworkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every CPO reachable through one of your roaming identities. Base networks are permanent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.createBase({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    emp_identity_id: 3,
    cpo_ids: ["NL*ABC", "BE*XYZ"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.BaseNetworkCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">getEffectiveView</a>({ ...params }) -> core.Page&lt;Evcloud.EffectiveCpo, Evcloud.EffectiveViewResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Each reachable CPO once: your own base networks first, then published networks in your ranking order.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.networks.getEffectiveView({
    limit: 50,
    country: "NL"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.networks.getEffectiveView({
    limit: 50,
    country: "NL"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetEffectiveViewNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">get</a>({ ...params }) -> Evcloud.NetworkDetailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

With how many locations and EVSEs it reaches today and how many token groups use it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.get({
    network_id: 21
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Base networks cannot be deleted. A sub-network assigned to token groups needs ``force=true``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.delete({
    network_id: 21,
    force: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.DeleteNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">update</a>({ ...params }) -> Evcloud.NetworkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Only the fields sent change. A base network's name and filters cannot change; its CPOs and access settings can.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.update({
    network_id: 21,
    cpo_ids: ["NL*ABC"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.NetworkPatch` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">listConsumers</a>({ ...params }) -> core.Page&lt;Evcloud.NetworkConsumer, Evcloud.NetworkConsumerPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Workspaces that ranked this base network, with its position in their ranking.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.networks.listConsumers({
    network_id: 20,
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.networks.listConsumers({
    network_id: 20,
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListConsumersNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">listLocations</a>({ ...params }) -> core.Page&lt;Evcloud.EmspGatewaySchemaNetworksLocationOut, Evcloud.EmspGatewaySchemaNetworksLocationPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Partner locations of its CPOs, with its filters and active access rules applied.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.networks.listLocations({
    network_id: 21,
    limit: 50,
    country: "NLD"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.networks.listLocations({
    network_id: 21,
    limit: 50,
    country: "NLD"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListLocationsNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">setPublishState</a>({ ...params }) -> Evcloud.NetworkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published base networks can be ranked by other workspaces. When withdrawing, ``unpublish_drain_until`` keeps their access until then.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.setPublishState({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    network_id: 20,
    published: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.PublishStateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">listRules</a>({ ...params }) -> core.Page&lt;Evcloud.NetworkRuleResponse, Evcloud.NetworkRulePage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

With no rules a network shows every location of its CPOs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.networks.listRules({
    network_id: 21,
    limit: 50,
    validity: "ACTIVE"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.networks.listRules({
    network_id: 21,
    limit: 50,
    validity: "ACTIVE"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListRulesNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">createRule</a>({ ...params }) -> Evcloud.NetworkRuleResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

INCLUDE shows only the listed locations, EXCLUDE hides them, optionally within an ``effective_from``/``effective_until`` window.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.createRule({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    network_id: 21,
    rule_type: "EXCLUDE",
    location_ids: ["LOC-AMS-001"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.NetworkRuleCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.networks.<a href="/src/api/resources/emsp/resources/networks/client/Client.ts">deleteRule</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes one access rule; the network's other rules stay in force.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.networks.deleteRule({
    network_id: 21,
    rule_id: 5
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.DeleteRuleNetworksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp EmpIdentities
<details><summary><code>client.emsp.empIdentities.<a href="/src/api/resources/emsp/resources/empIdentities/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.EmpIdentityOut, Evcloud.EmpIdentityPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The country code + party id pairs you issue tokens under.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.empIdentities.list({
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.empIdentities.list({
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListEmpIdentitiesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmpIdentitiesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.empIdentities.<a href="/src/api/resources/emsp/resources/empIdentities/client/Client.ts">register</a>({ ...params }) -> Evcloud.EmpIdentityOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds a country code + party id to issue tokens under. Each pair can be registered once.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.empIdentities.register({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    country_code: "BE",
    party_id: "OCP",
    label: "Belgium"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.EmpIdentityCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmpIdentitiesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.empIdentities.<a href="/src/api/resources/emsp/resources/empIdentities/client/Client.ts">get</a>({ ...params }) -> Evcloud.EmpIdentityOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One of your roaming identities.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.empIdentities.get({
    emp_identity_id: 3
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetEmpIdentitiesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmpIdentitiesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.empIdentities.<a href="/src/api/resources/emsp/resources/empIdentities/client/Client.ts">update</a>({ ...params }) -> Evcloud.EmpIdentityOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces label, contacts and default network access. Country code, party id and status cannot change.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.empIdentities.update({
    emp_identity_id: 3,
    label: "Primary",
    contact_email: "roaming@ev-cloud.com",
    default_network_access: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.EmpIdentityUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmpIdentitiesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.empIdentities.<a href="/src/api/resources/emsp/resources/empIdentities/client/Client.ts">deregister</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Refused with 409 for your last identity, or one that still has networks.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.empIdentities.deregister({
    emp_identity_id: 4
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.DeregisterEmpIdentitiesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmpIdentitiesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Tenant
<details><summary><code>client.emsp.tenant.<a href="/src/api/resources/emsp/resources/tenant/client/Client.ts">getProfile</a>() -> Evcloud.TenantProfileOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your display name, roaming identities and published-network ranking. The profile is created on first read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tenant.getProfile();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `TenantClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tenant.<a href="/src/api/resources/emsp/resources/tenant/client/Client.ts">updateProfile</a>({ ...params }) -> Evcloud.TenantProfileOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Only the display name can change; identities and ranking stay as they are.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tenant.updateProfile({
    display_name: "ev-cloud Mobility"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TenantProfileUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TenantClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tenant.<a href="/src/api/resources/emsp/resources/tenant/client/Client.ts">getPriority</a>() -> Evcloud.NetworkPriorityOrder</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Other workspaces' published base networks your drivers use, most preferred first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tenant.getPriority();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `TenantClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tenant.<a href="/src/api/resources/emsp/resources/tenant/client/Client.ts">setPriority</a>({ ...params }) -> Evcloud.NetworkPriorityOrder</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the whole ranking. Each id must be another workspace's published base network; when two networks reach the same CPO, the higher-ranked one wins.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tenant.setPriority({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    network_ids: [44, 51]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.NetworkPriorityOrderInput` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TenantClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp TokenGroups
<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.TokenGroupOut, Evcloud.TokenGroupPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your token groups with their members.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.tokenGroups.list({
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.tokenGroups.list({
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">create</a>({ ...params }) -> Evcloud.TokenGroupOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

An empty group; add tokens and assign networks to it afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.create({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    name: "Fleet cards",
    description: "Company cars"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TokenGroupCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">get</a>({ ...params }) -> Evcloud.TokenGroupOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One group with its members.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.get({
    group_id: 12
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">update</a>({ ...params }) -> Evcloud.TokenGroupOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename the group or replace its description; send ``description: null`` to clear it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.update({
    group_id: 12,
    name: "Fleet cards NL"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TokenGroupUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">activate</a>({ ...params }) -> Evcloud.TokenGroupActionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

PROVISIONED members are activated and SUSPENDED ones reactivated, and pushed to partners with ``valid: true``. Revoked members stay invalid.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.activate({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    group_id: 12
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ActivateTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">listNetworks</a>({ ...params }) -> core.Page&lt;Evcloud.TokenGroupNetworkOut, Evcloud.TokenGroupNetworkPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Member tokens reach the CPOs of these networks.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.tokenGroups.listNetworks({
    group_id: 12,
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.tokenGroups.listNetworks({
    group_id: 12,
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListNetworksTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">assignNetwork</a>({ ...params }) -> Evcloud.TokenGroupNetworkOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The group's tokens reach the network's CPOs, and the group can scope location searches.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.assignNetwork({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    group_id: 12,
    network_id: 21
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TokenGroupNetworkAssign` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">unassignNetwork</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The network itself is kept; only its assignment to the group is removed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.unassignNetwork({
    group_id: 12,
    network_id: 21
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.UnassignNetworkTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">reactivate</a>({ ...params }) -> Evcloud.TokenGroupActionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

SUSPENDED members are pushed to partners with ``valid: true`` again. Revoked members stay invalid.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.reactivate({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    group_id: 12
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ReactivateTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">revoke</a>({ ...params }) -> Evcloud.TokenGroupActionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every member that is not yet revoked is pushed with ``valid: false`` and marked revoked: later group activations leave it invalid.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.revoke({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    group_id: 12
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.RevokeTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">suspend</a>({ ...params }) -> Evcloud.TokenGroupActionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

ACTIVE members are pushed to partners with ``valid: false`` until the group is reactivated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.suspend({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    group_id: 12
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.SuspendTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">addTokens</a>({ ...params }) -> Evcloud.TokenGroupOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tokens already in the group are left as they are. Their ``valid`` flag is not changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.addTokens({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    group_id: 12,
    tokens: [{
            token_uid: "04A2B3C4D5E6F7",
            type: "RFID",
            ocpi_version: "221"
        }]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TokenGroupAddTokens` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokenGroups.<a href="/src/api/resources/emsp/resources/tokenGroups/client/Client.ts">removeToken</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The token keeps its current ``valid`` flag.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokenGroups.removeToken({
    group_id: 12,
    token_uid: "04A2B3C4D5E6F7",
    type: "RFID"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.RemoveTokenTokenGroupsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokenGroupsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Tokens
<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.TokenOut, Evcloud.TokenPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tokens you issued, filtered by status, type or text in uid, contract id or printed number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.tokens.list({
    limit: 50,
    status: "ACTIVE",
    type: "RFID"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.tokens.list({
    limit: 50,
    status: "ACTIVE",
    type: "RFID"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">provision</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates the token as PROVISIONED; with ``auto_activate`` it is pushed to roaming partners and stored ACTIVE. If the push to roaming partners fails the call answers 502 and the token is left as it was; retry with the same Idempotency-Key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.provision({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    body: {
        uid: "04A2B3C4D5E6F7",
        type: "RFID",
        contract_id: "NL-OCP-C12345678-X",
        issuer: "ev-cloud Mobility",
        visual_number: "OCP-0001",
        language: "nl",
        metadata: {
            "driver_id": "drv-123"
        },
        auto_activate: true
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ProvisionTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">bulkProvision</a>({ ...params }) -> Evcloud.TokenBulkOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The batch is validated and created as a whole. With ``auto_activate`` each token is pushed in turn; a failed push is listed and that token stays PROVISIONED.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.bulkProvision({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    tokens: [{
            uid: "04A2B3C4D5E6F7",
            type: "RFID",
            contract_id: "NL-OCP-C12345678-X",
            issuer: "ev-cloud Mobility",
            visual_number: "OCP-0001",
            language: "nl",
            metadata: {
                "driver_id": "drv-123"
            },
            auto_activate: true
        }, {
            uid: "04A2B3C4D5E6F8",
            type: "RFID",
            contract_id: "NL-OCP-C12345678-X",
            issuer: "ev-cloud Mobility",
            visual_number: "OCP-0002",
            language: "nl",
            metadata: {
                "driver_id": "drv-123"
            },
            auto_activate: true
        }]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TokenBulkCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">get</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One token you issued.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.get({
    token_id: 77
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">update</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Only the fields sent change. ACTIVE and SUSPENDED tokens are pushed to partners again before the change is saved. If the push to roaming partners fails the call answers 502 and the token is left as it was; retry with the same Idempotency-Key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.update({
    token_id: 77,
    visual_number: "OCP-0002"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.TokenUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">activate</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

PROVISIONED → ACTIVE: pushed to partners with ``valid: true``. If the push to roaming partners fails the call answers 502 and the token is left as it was; retry with the same Idempotency-Key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.activate({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    token_id: 77
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ActivateTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">history</a>({ ...params }) -> core.Page&lt;Evcloud.TokenEventOut, Evcloud.TokenEventPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lifecycle changes of the token, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.tokens.history({
    token_id: 77,
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.tokens.history({
    token_id: 77,
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.HistoryTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">reactivate</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

SUSPENDED → ACTIVE: pushed to partners with ``valid: true``. If the push to roaming partners fails the call answers 502 and the token is left as it was; retry with the same Idempotency-Key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.reactivate({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    token_id: 77
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ReactivateTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">revoke</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Final: any status except REVOKED. A token partners already have is pushed with ``valid: false`` first. If the push to roaming partners fails the call answers 502 and the token is left as it was; retry with the same Idempotency-Key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.revoke({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    token_id: 77,
    body: {
        reason: "Contract ended"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.RevokeTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tokens.<a href="/src/api/resources/emsp/resources/tokens/client/Client.ts">suspend</a>({ ...params }) -> Evcloud.TokenOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

ACTIVE → SUSPENDED: pushed to partners with ``valid: false``. If the push to roaming partners fails the call answers 502 and the token is left as it was; retry with the same Idempotency-Key.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tokens.suspend({
    "Idempotency-Key": "5d1f7c2e-8b3a-4e6f-9c0d-1a2b3c4d5e6f",
    token_id: 77,
    body: {
        reason: "Reported lost"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.SuspendTokensRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TokensClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Evses
<details><summary><code>client.emsp.evses.<a href="/src/api/resources/emsp/resources/evses/client/Client.ts">status</a>({ ...params }) -> Evcloud.EvseStatusOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Status of one EVSE with its connectors and capabilities, read live. Poll this before a remote start; it is never cached.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.evses.status({
    location_id: "LOC-AMS-001",
    evse_uid: "EVSE-AMS-001-1",
    country_code: "NL",
    party_id: "ABC"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.StatusEvsesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EvsesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Tariffs
<details><summary><code>client.emsp.tariffs.<a href="/src/api/resources/emsp/resources/tariffs/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.Tariff, Evcloud.EmspTariffPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tariffs of the CPOs you reach, in OCPI 2.2.1 shape whatever version the CPO spoke, optionally for one CPO.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.tariffs.list({
    limit: 50,
    country_code: "NL",
    party_id: "ABC"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.tariffs.list({
    limit: 50,
    country_code: "NL",
    party_id: "ABC"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListTariffsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tariffs.<a href="/src/api/resources/emsp/resources/tariffs/client/Client.ts">get</a>({ ...params }) -> Evcloud.Tariff</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One tariff in OCPI 2.2.1 shape, addressed by the CPO's country code and party id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tariffs.get({
    tariff_id: "TARIFF-DC-FAST",
    country_code: "NL",
    party_id: "ABC"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetTariffsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.tariffs.<a href="/src/api/resources/emsp/resources/tariffs/client/Client.ts">estimate</a>({ ...params }) -> Evcloud.EstimateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Prices a session on one connector from its tariff: energy, time, flat fee and parking lines, totals with and without VAT, and display strings.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.tariffs.estimate({
    location: {
        country_code: "NL",
        party_id: "ABC",
        location_id: "LOC-AMS-001"
    },
    evse_uid: "EVSE-AMS-001-1",
    connector_id: "1",
    kwh: "30"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.EstimateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `TariffsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Chargers
<details><summary><code>client.emsp.chargers.<a href="/src/api/resources/emsp/resources/chargers/client/Client.ts">resolve</a>({ ...params }) -> Evcloud.ResolveChargersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

``own``: your OCPP charger, commanded through ocpp-api-gateway. ``roaming``: a partner CPO, commanded over OCPI in ``ocpi_version``. For support and debugging; sending a command (``POST /emsp/commands/{authorization_reference}/{command}``) resolves by itself.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.chargers.resolve({
    country_code: "DE",
    party_id: "ENA",
    location_id: "LOC-1",
    evse_uid: "LOC-1-E1",
    connector_id: "1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ResolveRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Commands
<details><summary><code>client.emsp.commands.<a href="/src/api/resources/emsp/resources/commands/client/Client.ts">send</a>({ ...params }) -> Evcloud.CommandAccepted</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Starts, stops, unlocks or reserves. ``response`` is the immediate answer; the final result arrives on ``X-Command-Callback-Url`` and on ``GET /emsp/commands/{tracking_id}``. ``X-Tracking-Id`` (or ``Idempotency-Key``) makes the call safe to retry: the same id returns the first outcome without sending again.

emsp-gateway decides whether the charger is yours (sent over OCPP) or a roaming CPO's (sent over OCPI in the partner's version); ``route`` says which. Session and CDR updates for this authorization go to the session and CDR callback URLs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.commands.send({
    "X-Tracking-Id": "6f1c2b0e-3c4d-4e5f-8a9b-0c1d2e3f4a5b",
    "X-Command-Callback-Url": "https://api.easyplug.example/hooks/command",
    "X-Session-Callback-Url": "https://api.easyplug.example/hooks/session",
    "X-Cdr-Callback-Url": "https://api.easyplug.example/hooks/cdr",
    authorization_reference: "EZP-AUTH-0001",
    command: "START_SESSION",
    token: {
        uid: "DRIVER-1",
        type: "APP_USER",
        contract_id: "FR-EZP-C00000001-4"
    },
    location_id: "LOC-1",
    evse_uid: "LOC-1-E1",
    connector_id: "1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.EmspCommandBody` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommandsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.commands.<a href="/src/api/resources/emsp/resources/commands/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.CommandRecord, Evcloud.CommandPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Commands you sent, oldest first, optionally for one authorization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.commands.list({
    limit: 50,
    authorization_reference: "EZP-AUTH-0001"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.commands.list({
    limit: 50,
    authorization_reference: "EZP-AUTH-0001"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListCommandsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommandsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.commands.<a href="/src/api/resources/emsp/resources/commands/client/Client.ts">get</a>({ ...params }) -> Evcloud.CommandRecord</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Route, status, the immediate response and the final result of one command. A roaming command still ``PENDING`` is refreshed from the partner's CommandResult first, so polling this finishes it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.commands.get({
    tracking_id: "6f1c2b0e-3c4d-4e5f-8a9b-0c1d2e3f4a5b"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetCommandsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommandsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Sessions
<details><summary><code>client.emsp.sessions.<a href="/src/api/resources/emsp/resources/sessions/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.EmspSessionOut, Evcloud.EmspSessionPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sessions of your drivers on your own chargers and at partner CPOs, filtered by authorization, token, status or start time.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.sessions.list({
    limit: 50,
    authorization_reference: "EZP-AUTH-0001"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.sessions.list({
    limit: 50,
    authorization_reference: "EZP-AUTH-0001"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.sessions.<a href="/src/api/resources/emsp/resources/sessions/client/Client.ts">get</a>({ ...params }) -> Evcloud.EmspSessionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One session: energy, cost, status. Send country_code and party_id when two parties used the id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.sessions.get({
    session_id: "SESS-1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Emsp Cdrs
<details><summary><code>client.emsp.cdrs.<a href="/src/api/resources/emsp/resources/cdrs/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.EmspCdrOut, Evcloud.EmspCdrPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Charge detail records of your drivers, filtered by authorization, session, token or start time.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.emsp.cdrs.list({
    limit: 50,
    session_id: "SESS-1"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.emsp.cdrs.list({
    limit: 50,
    session_id: "SESS-1"
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.ListCdrsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CdrsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.emsp.cdrs.<a href="/src/api/resources/emsp/resources/cdrs/client/Client.ts">get</a>({ ...params }) -> Evcloud.EmspCdrOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One CDR with its tariffs and totals. Send country_code and party_id when two parties used the id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.emsp.cdrs.get({
    cdr_id: "CDR-1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.emsp.GetCdrsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CdrsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Energy ControlRequests
<details><summary><code>client.energy.controlRequests.<a href="/src/api/resources/energy/resources/controlRequests/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.ControlRequestResponse, Evcloud.ControlRequestPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your workspace's limit requests, newest first. PENDING requests are resolved within seconds of the charger answering.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.energy.controlRequests.list({
    charge_point_id: "CP-AMS-001",
    result: "ACCEPTED",
    offset: 0,
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.energy.controlRequests.list({
    charge_point_id: "CP-AMS-001",
    result: "ACCEPTED",
    offset: 0,
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.energy.ListControlRequestsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ControlRequestsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.energy.controlRequests.<a href="/src/api/resources/energy/resources/controlRequests/client/Client.ts">create</a>({ ...params }) -> Evcloud.ControlRequestResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends an OCPP charging profile to the charger. The result is PENDING until the charger answers: read it back with ``GET /energy-management/control-requests/{request_id}``, or subscribe a webhook to ``energy.control_response``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.energy.controlRequests.create({
    "Idempotency-Key": "limit-cp-ams-001-2026-10-03T10:00",
    charge_point_id: "CP-AMS-001",
    action: "SET_EVSE_INPUT_LIMIT",
    connector_id: 0,
    limit: 11000,
    unit: "W",
    valid_to: "2026-10-03T18:00:00Z"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.energy.ControlRequestCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ControlRequestsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.energy.controlRequests.<a href="/src/api/resources/energy/resources/controlRequests/client/Client.ts">get</a>({ ...params }) -> Evcloud.ControlRequestResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

While the request is PENDING, the charger's answer is checked on read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.energy.controlRequests.get({
    request_id: "6b1f2c3d-4e5f-4a6b-8c7d-9e0f1a2b3c4d"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.energy.GetControlRequestsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ControlRequestsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Energy Health
<details><summary><code>client.energy.health.<a href="/src/api/resources/energy/resources/health/client/Client.ts">get</a>() -> Evcloud.HealthOk</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Answers ``ok`` when the energy management service is up.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.energy.health.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Energy PowerMeasurements
<details><summary><code>client.energy.powerMeasurements.<a href="/src/api/resources/energy/resources/powerMeasurements/client/Client.ts">list</a>({ ...params }) -> Evcloud.PowerMeasurementList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Active import power the charger reported, in kW, newest first. ``date_from`` is inclusive and ``date_to`` exclusive. Returns at most ``limit`` readings with no next page: move the date window to read older ones.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.energy.powerMeasurements.list({
    charge_point_id: "CP-AMS-001",
    connector_id: 1,
    date_from: "2026-10-03T00:00:00Z",
    limit: 50
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.energy.ListPowerMeasurementsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PowerMeasurementsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.energy.powerMeasurements.<a href="/src/api/resources/energy/resources/powerMeasurements/client/Client.ts">latest</a>({ ...params }) -> Evcloud.PowerMeasurementList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The newest active power reading of each connector on the charger, in kW.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.energy.powerMeasurements.latest({
    charge_point_id: "CP-AMS-001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.energy.LatestPowerMeasurementsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PowerMeasurementsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ocpi Invites
<details><summary><code>client.ocpi.invites.<a href="/src/api/resources/ocpi/resources/invites/client/Client.ts">create</a>({ ...params }) -> Evcloud.PartnerInviteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns Token A and the handshake URLs to hand to the partner, once.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.invites.create({
    country_code: "DE",
    party_id: "EMS",
    role: "EMSP",
    version: "2.2.1",
    expires_days: 30
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PartnerInviteCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InvitesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.invites.<a href="/src/api/resources/ocpi/resources/invites/client/Client.ts">rotate</a>({ ...params }) -> Evcloud.PartnerInviteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Issues a new Token A for a pending invite and invalidates the old one; send the new token to the partner.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.invites.rotate({
    invite_id: 12,
    expires_days: 14
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PartnerInviteUpdateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InvitesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.invites.<a href="/src/api/resources/ocpi/resources/invites/client/Client.ts">revoke</a>({ ...params }) -> Evcloud.PartnerInviteRevokeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Revokes a pending invite so its Token A can no longer start a credentials handshake.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.invites.revoke({
    invite_id: 12
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.RevokeInvitesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InvitesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ocpi Partners
<details><summary><code>client.ocpi.partners.<a href="/src/api/resources/ocpi/resources/partners/client/Client.ts">list</a>({ ...params }) -> Evcloud.PartnerResponse[]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists this workspace's roaming partners, one row per partner role (operation). Each row's ``roaming_partner_id`` is the id the sync operations take.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.partners.list({
    role: "EMSP"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.ListPartnersRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PartnersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.partners.<a href="/src/api/resources/ocpi/resources/partners/client/Client.ts">register</a>({ ...params }) -> Evcloud.PartnerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a roaming partner role (country_code, party_id, role, OCPI version) for this workspace and links it to a ``roaming_partner_id``. Run the credentials handshake next with ``ocpi_start_credentials_handshake``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.partners.register({
    country_code: "DE",
    party_id: "EMS",
    role: "EMSP",
    ocpi_version: "2.2.1",
    partner_name: "Example eMSP GmbH"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PartnerRegisterRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PartnersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.partners.<a href="/src/api/resources/ocpi/resources/partners/client/Client.ts">get</a>({ ...params }) -> Evcloud.PartnerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one roaming partner operation by its id. 404 if it does not belong to this workspace.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.partners.get({
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.GetPartnersRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PartnersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.partners.<a href="/src/api/resources/ocpi/resources/partners/client/Client.ts">remove</a>({ ...params }) -> Evcloud.PartnerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Soft-deletes the partner; its OCPI traffic stops. Admin role required.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.partners.remove({
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.RemovePartnersRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PartnersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.partners.<a href="/src/api/resources/ocpi/resources/partners/client/Client.ts">update</a>({ ...params }) -> Evcloud.PartnerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a roaming partner's role, version, name or active flag. Only the fields sent change; send ``expected_revision`` to refuse the update if the row changed since you read it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.partners.update({
    partner_id: 7,
    partner_name: "Example eMSP AG"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PartnerUpdateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PartnersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ocpi Credentials
<details><summary><code>client.ocpi.credentials.<a href="/src/api/resources/ocpi/resources/credentials/client/Client.ts">status</a>({ ...params }) -> Evcloud.CredentialsHandshakeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the stored handshake with a partner for the path version and role: its endpoints, token state and last exchange.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.credentials.status({
    version: "221",
    role: "cpo",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.StatusCredentialsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CredentialsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.credentials.<a href="/src/api/resources/ocpi/resources/credentials/client/Client.ts">startHandshake</a>({ ...params }) -> Evcloud.CredentialsHandshakeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Runs the OCPI credentials handshake with a partner of the caller's workspace for the path version and role: fetches its versions with Token A, then exchanges Token B for Token C.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.credentials.startHandshake({
    version: "221",
    role: "cpo",
    body: {
        partner_id: 7,
        partner_url: "https://emsp.example.com/ocpi/versions",
        partner_token: "partner-token-a"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.StartHandshakeCredentialsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CredentialsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.credentials.<a href="/src/api/resources/ocpi/resources/credentials/client/Client.ts">rotate</a>({ ...params }) -> Evcloud.CredentialsHandshakeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Re-runs the credentials exchange with an already registered partner so both sides get fresh tokens.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.credentials.rotate({
    version: "221",
    role: "cpo",
    body: {
        partner_id: 7
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.RotateCredentialsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CredentialsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.credentials.<a href="/src/api/resources/ocpi/resources/credentials/client/Client.ts">unregister</a>({ ...params }) -> Evcloud.CredentialsHandshakeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the credentials with a partner for the path version and role; it can no longer call us and we stop calling it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.credentials.unregister({
    version: "221",
    role: "cpo",
    body: {
        partner_id: 7
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UnregisterCredentialsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CredentialsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.credentials.<a href="/src/api/resources/ocpi/resources/credentials/client/Client.ts">pullVersions</a>({ ...params }) -> Evcloud.PartnerVersionsPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Calls the partner's versions and version-details endpoints and stores the modules it offers, without changing credentials.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.credentials.pullVersions({
    version: "221",
    role: "cpo",
    partner_url: "https://emsp.example.com/ocpi/versions",
    partner_token: "partner-token-a"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PartnerVersionsPullRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CredentialsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ocpi CpoData
<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">upsertLocation</a>({ ...params }) -> Evcloud.LocationWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stores a full OCPI Location for the path version, replacing any existing one with the same id. The owner country_code and party_id are set to this workspace's own identity. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.upsertLocation({
    version: "221",
    push_to_partner_id: 7,
    body: {
        "id": "LOC-AMS-1",
        "publish": true,
        "name": "Amsterdam depot",
        "address": "Stationsplein 1",
        "city": "Amsterdam",
        "postal_code": "1012 AB",
        "country": "NLD",
        "coordinates": {
            "latitude": "52.379189",
            "longitude": "4.899431"
        },
        "time_zone": "Europe/Amsterdam",
        "evses": [
            {
                "uid": "EVSE-AMS-1-1",
                "evse_id": "NL*OCP*E0001*1",
                "status": "AVAILABLE",
                "connectors": [
                    {
                        "id": "1",
                        "standard": "IEC_62196_T2",
                        "format": "SOCKET",
                        "power_type": "AC_3_PHASE",
                        "max_voltage": 230,
                        "max_amperage": 32,
                        "last_updated": "2026-09-30T10:00:00Z"
                    }
                ],
                "last_updated": "2026-09-30T10:00:00Z"
            }
        ],
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpsertLocationCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">updateLocation</a>({ ...params }) -> Evcloud.LocationWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies a partial OCPI Location (PATCH semantics) to a stored location; include ``last_updated``. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.updateLocation({
    version: "221",
    location_id: "LOC-AMS-1",
    body: {
        "name": "Amsterdam Centraal depot",
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpdateLocationCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">updateEvseStatus</a>({ ...params }) -> Evcloud.EvseStatusWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A charger StatusNotification in roaming is this patch. ``broadcast=true`` sends it to every active eMSP and hub.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.updateEvseStatus({
    version: "221",
    location_id: "LOC-AMS-1",
    evse_uid: "EVSE-AMS-1-1",
    body: {
        "status": "CHARGING",
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpdateEvseStatusCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">updateConnector</a>({ ...params }) -> Evcloud.ConnectorWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies a partial OCPI Connector to a connector of a stored location's EVSE; include ``last_updated``. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.updateConnector({
    version: "221",
    location_id: "LOC-AMS-1",
    evse_uid: "EVSE-AMS-1-1",
    connector_id: "1",
    body: {
        "tariff_ids": [
            "TARIFF-AC-STD"
        ],
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpdateConnectorCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">upsertSession</a>({ ...params }) -> Evcloud.SessionWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stores a full OCPI Session for the path version, replacing any existing one with the same id. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.upsertSession({
    version: "221",
    body: {
        "id": "SES-20260930-0001",
        "start_date_time": "2026-09-30T10:00:00Z",
        "kwh": 11.5,
        "cdr_token": {
            "country_code": "DE",
            "party_id": "EMS",
            "uid": "04A2B3C4D5E6F7",
            "type": "RFID",
            "contract_id": "DE-EMS-C12345678-X"
        },
        "auth_method": "WHITELIST",
        "location_id": "LOC-AMS-1",
        "evse_uid": "EVSE-AMS-1-1",
        "connector_id": "1",
        "currency": "EUR",
        "status": "ACTIVE",
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpsertSessionCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">updateSession</a>({ ...params }) -> Evcloud.SessionWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies a partial OCPI Session (for example new kwh or status) to a stored session; include ``last_updated``. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.updateSession({
    version: "221",
    session_id: "SES-20260930-0001",
    body: {
        "kwh": 18.2,
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpdateSessionCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">createCdr</a>({ ...params }) -> Evcloud.CdrWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stores a CDR (charge detail record), the billed record of a finished session. CDRs cannot be changed once created. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.createCdr({
    version: "221",
    body: {
        "id": "CDR-20260930-0001",
        "start_date_time": "2026-09-30T08:00:00Z",
        "end_date_time": "2026-09-30T10:00:00Z",
        "session_id": "SES-20260930-0001",
        "cdr_token": {
            "country_code": "DE",
            "party_id": "EMS",
            "uid": "04A2B3C4D5E6F7",
            "type": "RFID",
            "contract_id": "DE-EMS-C12345678-X"
        },
        "auth_method": "WHITELIST",
        "cdr_location": {
            "id": "LOC-AMS-1",
            "address": "Stationsplein 1",
            "city": "Amsterdam",
            "country": "NLD",
            "coordinates": {
                "latitude": "52.379189",
                "longitude": "4.899431"
            },
            "evse_uid": "EVSE-AMS-1-1",
            "evse_id": "NL*OCP*E0001*1",
            "connector_id": "1",
            "connector_standard": "IEC_62196_T2",
            "connector_format": "SOCKET",
            "connector_power_type": "AC_3_PHASE"
        },
        "currency": "EUR",
        "charging_periods": [
            {
                "start_date_time": "2026-09-30T08:00:00Z",
                "dimensions": [
                    {
                        "type": "ENERGY",
                        "volume": 22
                    }
                ]
            }
        ],
        "total_cost": {
            "before_taxes": 7.7,
            "taxes": [
                {
                    "name": "VAT",
                    "amount": 1.62
                }
            ]
        },
        "total_energy": 22,
        "total_time": 2,
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.CreateCdrCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">upsertTariff</a>({ ...params }) -> Evcloud.TariffWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stores a full OCPI Tariff for the path version, replacing any existing one with the same id. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.upsertTariff({
    version: "221",
    body: {
        "id": "TARIFF-AC-STD",
        "currency": "EUR",
        "type": "REGULAR",
        "tax_included": "NO",
        "elements": [
            {
                "price_components": [
                    {
                        "type": "ENERGY",
                        "price": 0.35,
                        "vat": 21,
                        "step_size": 1
                    }
                ]
            }
        ],
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpsertTariffCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">deleteTariff</a>({ ...params }) -> Evcloud.TariffDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Soft-deletes a stored tariff. Pass ``push_to_partner_id`` to also send the DELETE to that partner eMSP.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.deleteTariff({
    version: "221",
    tariff_id: "TARIFF-AC-STD"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.DeleteTariffCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">cancelReservation</a>({ ...params }) -> Evcloud.ReservationCancelResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancels a reservation made on one of our chargers and sends the eMSP the cancellation. OCPI 2.2.1 and 2.3.0 only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.cancelReservation({
    version: "221",
    ocpp_reservation_id: 1042
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.CancelReservationCpoDataRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.cpoData.<a href="/src/api/resources/ocpi/resources/cpoData/client/Client.ts">sendActiveChargingProfile</a>({ ...params }) -> Evcloud.ChargingProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends the eMSP the charging profile currently active on one of its sessions (the CPO's ActiveChargingProfile callback). OCPI 2.2.1 and 2.3.0 only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.cpoData.sendActiveChargingProfile({
    version: "221",
    session_id: "SES-20260930-0001",
    partner_id: 7,
    start_date_time: "2026-09-30T10:00:00Z",
    charging_profile: {
        charging_rate_unit: "A",
        charging_profile_period: [{
                start_period: 0,
                limit: 16
            }, {
                start_period: 3600,
                limit: 32
            }]
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.ActiveChargingProfileRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CpoDataClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ocpi Emsp
<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">upsertToken</a>({ ...params }) -> Evcloud.TokenWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stores a full OCPI Token on our eMSP side, replacing any existing one with the same uid. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.upsertToken({
    version: "221",
    body: {
        "country_code": "DE",
        "party_id": "EMS",
        "uid": "04A2B3C4D5E6F7",
        "type": "RFID",
        "contract_id": "DE-EMS-C12345678-X",
        "issuer": "Example eMSP GmbH",
        "valid": true,
        "whitelist": "ALLOWED",
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpsertTokenEmspRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">updateToken</a>({ ...params }) -> Evcloud.TokenWriteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies a partial OCPI Token to a stored token, for example ``valid=false`` to block it; include ``last_updated``. Pass ``push_to_partner_id`` to also push it to that partner right away.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.updateToken({
    version: "221",
    token_uid: "04A2B3C4D5E6F7",
    type: "RFID",
    body: {
        "valid": false,
        "last_updated": "2026-09-30T10:00:00Z"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.UpdateTokenEmspRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">sendCommand</a>({ ...params }) -> Evcloud.CommandSendResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the CPO's immediate CommandResponse. The async CommandResult is delivered to the OCPI gateway's own callback; clients cannot set ``response_url``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.sendCommand({
    version: "221",
    command: "START_SESSION",
    partner_id: 7,
    token: {
        "country_code": "DE",
        "party_id": "EMS",
        "uid": "04A2B3C4D5E6F7",
        "type": "RFID",
        "contract_id": "DE-EMS-C12345678-X",
        "issuer": "Example eMSP GmbH",
        "valid": true,
        "whitelist": "ALLOWED",
        "last_updated": "2026-09-30T10:00:00Z"
    },
    location_id: "LOC-AMS-1",
    evse_uid: "EVSE-AMS-1-1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.CommandSendRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">setChargingPreferences</a>({ ...params }) -> Evcloud.ChargingPreferencesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends the CPO charging preferences (profile type, departure time, energy need) for a session it runs. OCPI 2.2.1 and 2.3.0 only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.setChargingPreferences({
    version: "221",
    session_id: "SES-20260930-0001",
    partner_id: 7,
    profile_type: "CHEAP",
    departure_time: "2026-10-01T07:00:00Z",
    energy_need: 30
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.ChargingPreferencesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">getActiveChargingProfile</a>({ ...params }) -> Evcloud.ChargingProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Asks the CPO for the charging profile active on a session it runs. The result arrives asynchronously. OCPI 2.2.1 and 2.3.0 only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.getActiveChargingProfile({
    version: "221",
    session_id: "SES-20260930-0001",
    partner_id: 7,
    duration: 3600
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.GetActiveChargingProfileEmspRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">setChargingProfile</a>({ ...params }) -> Evcloud.ChargingProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Asks the CPO to apply a charging profile to a session it runs. The CPO answers asynchronously. OCPI 2.2.1 and 2.3.0 only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.setChargingProfile({
    version: "221",
    session_id: "SES-20260930-0001",
    partner_id: 7,
    charging_profile: {
        charging_rate_unit: "A",
        charging_profile_period: [{
                start_period: 0,
                limit: 16
            }, {
                start_period: 3600,
                limit: 32
            }]
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.ChargingProfileSetRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.emsp.<a href="/src/api/resources/ocpi/resources/emsp/client/Client.ts">clearChargingProfile</a>({ ...params }) -> Evcloud.ChargingProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Asks the CPO to remove the charging profile set on a session it runs. OCPI 2.2.1 and 2.3.0 only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.emsp.clearChargingProfile({
    version: "221",
    session_id: "SES-20260930-0001",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.ClearChargingProfileEmspRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EmspClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ocpi Sync
<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pushLocation</a>({ ...params }) -> Evcloud.SyncPushResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a stored location to a partner eMSP (PUT to its Locations module). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pushLocation({
    version: "221",
    location_id: "LOC-AMS-1",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PushLocationSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pushCdr</a>({ ...params }) -> Evcloud.SyncPushResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a stored CDR to a partner eMSP (POST to its CDRs module). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pushCdr({
    version: "221",
    cdr_id: "CDR-20260930-0001",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PushCdrSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pushTariff</a>({ ...params }) -> Evcloud.SyncPushResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a stored tariff to a partner eMSP (PUT to its Tariffs module). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pushTariff({
    version: "221",
    tariff_id: "TARIFF-AC-STD",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PushTariffSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pushSession</a>({ ...params }) -> Evcloud.SyncPushResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a stored session to a partner eMSP: the full object, or only ``patch_body`` as a PATCH. ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pushSession({
    version: "221",
    session_id: "SES-20260930-0001",
    partner_id: 7,
    body: {
        patch_body: {
            "kwh": 18.2,
            "last_updated": "2026-09-30T10:00:00Z"
        }
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PushSessionSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pushToken</a>({ ...params }) -> Evcloud.SyncPushResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a stored token to a partner CPO: the full object, or only ``patch_body`` as a PATCH. ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pushToken({
    version: "221",
    token_uid: "04A2B3C4D5E6F7",
    partner_id: 7,
    type: "RFID",
    body: {
        patch_body: {
            "valid": false,
            "last_updated": "2026-09-30T10:00:00Z"
        }
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PushTokenSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullTokens</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches tokens from a partner eMSP's Tokens module, page by page. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync (``date_from`` is then ignored). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullTokens({
    version: "221",
    partner_id: 7,
    date_from: "2026-09-29T00:00:00Z",
    limit: 500
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullTokensSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullLocations</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches locations from a partner CPO's Locations module, page by page. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync (``date_from`` is then ignored). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullLocations({
    version: "221",
    partner_id: 7,
    date_from: "2026-09-29T00:00:00Z",
    limit: 500
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullLocationsSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullSessions</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches sessions from a partner CPO's Sessions module, page by page. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync (``date_from`` is then ignored). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullSessions({
    version: "221",
    partner_id: 7,
    date_from: "2026-09-29T00:00:00Z",
    limit: 500
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullSessionsSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullCdrs</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches CDRs from a partner CPO's CDRs module, page by page. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync. ``date_from`` is then ignored. ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullCdrs({
    version: "221",
    partner_id: 7,
    date_from: "2026-09-29T00:00:00Z",
    limit: 500
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullCdrsSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullTariffs</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches tariffs from a partner CPO's Tariffs module, page by page. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync (``date_from`` is then ignored). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullTariffs({
    version: "221",
    partner_id: 7,
    date_from: "2026-09-29T00:00:00Z",
    limit: 500
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullTariffsSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullHubClientInfoAsEmsp</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches a Hub's ClientInfo list (which parties are reachable through it) into our eMSP side. OCPI 2.2.1 and 2.3.0 only. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync (``date_from`` is then ignored). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullHubClientInfoAsEmsp({
    version: "221",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullHubClientInfoAsEmspSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ocpi.sync.<a href="/src/api/resources/ocpi/resources/sync/client/Client.ts">pullHubClientInfoAsCpo</a>({ ...params }) -> Evcloud.SyncPullResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetches a Hub's ClientInfo list (which parties are reachable through it) into our CPO side. OCPI 2.2.1 and 2.3.0 only. Results are stored in the OCPI store. Pulls are incremental from the last sync; set ``full_replace=true`` for a full resync (``date_from`` is then ignored). ``partner_id`` is the roaming partner id (``roaming_partner_id``), not the operation id from ``GET /ocpi/partners``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.ocpi.sync.pullHubClientInfoAsCpo({
    version: "221",
    partner_id: 7
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.ocpi.PullHubClientInfoAsCpoSyncRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `SyncClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy Backends
<details><summary><code>client.proxy.backends.<a href="/src/api/resources/proxy/resources/backends/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.BackendOut, Evcloud.BackendPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your workspace's CSMS backends, by priority. Auth header values are never returned.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.backends.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.backends.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListBackendsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.backends.<a href="/src/api/resources/proxy/resources/backends/client/Client.ts">create</a>({ ...params }) -> Evcloud.BackendOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. ``auth`` takes header values and TLS file paths; they are stored but never returned. TLS needs a ``wss://`` url.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.backends.create({
    name: "primary-csms",
    url: "wss://csms.example.com/ocpp",
    priority: 100,
    auth: {
        "headers": {
            "Authorization": "Bearer <token>"
        }
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.BackendCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.backends.<a href="/src/api/resources/proxy/resources/backends/client/Client.ts">getByName</a>({ ...params }) -> Evcloud.BackendOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Backend names are unique in your workspace.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.backends.getByName({
    name: "primary-csms"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetByNameBackendsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.backends.<a href="/src/api/resources/proxy/resources/backends/client/Client.ts">get</a>({ ...params }) -> Evcloud.BackendOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One backend of your workspace.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.backends.get({
    backend_id: "3fa85f64-5717-4562-b3fc-2c963f66afa6"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetBackendsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.backends.<a href="/src/api/resources/proxy/resources/backends/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.backends.delete({
    backend_id: "backend_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.DeleteBackendsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.backends.<a href="/src/api/resources/proxy/resources/backends/client/Client.ts">update</a>({ ...params }) -> Evcloud.BackendOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Send ``expected_revision`` to refuse the write (409) if the row changed since you read it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.backends.update({
    backend_id: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    enabled: false,
    expected_revision: 1
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.BackendUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy RoutingPolicies
<details><summary><code>client.proxy.routingPolicies.<a href="/src/api/resources/proxy/resources/routingPolicies/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.RoutingPolicyOut, Evcloud.RoutingPolicyPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uplink (station to CSMS) and downlink (CSMS to station) policies of your chargers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.routingPolicies.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.routingPolicies.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListRoutingPoliciesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingPoliciesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingPolicies.<a href="/src/api/resources/proxy/resources/routingPolicies/client/Client.ts">create</a>({ ...params }) -> Evcloud.RoutingPolicyOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Uplink policies set ``role`` (``owner`` answers the charger, ``mirror`` only receives); downlink policies set ``allowed``. The backend needs a routing rule for the charger.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingPolicies.create({
    charge_point_id: "CP-AMS-001",
    backend_id: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    direction: "uplink",
    role: "owner"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.RoutingPolicyCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingPoliciesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingPolicies.<a href="/src/api/resources/proxy/resources/routingPolicies/client/Client.ts">get</a>({ ...params }) -> Evcloud.RoutingPolicyOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One routing policy of your workspace.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingPolicies.get({
    routing_policy_id: "7c9e6679-7425-40de-944b-e07fc1f90ae7"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetRoutingPoliciesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingPoliciesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingPolicies.<a href="/src/api/resources/proxy/resources/routingPolicies/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingPolicies.delete({
    routing_policy_id: "routing_policy_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.DeleteRoutingPoliciesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingPoliciesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingPolicies.<a href="/src/api/resources/proxy/resources/routingPolicies/client/Client.ts">update</a>({ ...params }) -> Evcloud.RoutingPolicyOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Send ``expected_revision`` to refuse the write (409) if the row changed since you read it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingPolicies.update({
    routing_policy_id: "7c9e6679-7425-40de-944b-e07fc1f90ae7",
    role: "mirror"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.RoutingPolicyUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingPoliciesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy RoutingRules
<details><summary><code>client.proxy.routingRules.<a href="/src/api/resources/proxy/resources/routingRules/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.RoutingRuleOut, Evcloud.RoutingRulePage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Which backends each charger is routed to, lowest ``priority`` first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.routingRules.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.routingRules.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListRoutingRulesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingRulesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingRules.<a href="/src/api/resources/proxy/resources/routingRules/client/Client.ts">create</a>({ ...params }) -> Evcloud.RoutingRuleOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Routes a charger to a backend; ``downlink_actions`` limits the CALLs that backend may send.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingRules.create({
    charge_point_id: "CP-AMS-001",
    backend_id: "3fa85f64-5717-4562-b3fc-2c963f66afa6"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.RoutingRuleCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingRulesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingRules.<a href="/src/api/resources/proxy/resources/routingRules/client/Client.ts">get</a>({ ...params }) -> Evcloud.RoutingRuleOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One routing rule of your workspace.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingRules.get({
    routing_rule_id: "5b2f8d4e-1a3c-4e6f-8b7d-9c0a1e2f3b4d"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetRoutingRulesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingRulesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingRules.<a href="/src/api/resources/proxy/resources/routingRules/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingRules.delete({
    routing_rule_id: "routing_rule_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.DeleteRoutingRulesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingRulesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.routingRules.<a href="/src/api/resources/proxy/resources/routingRules/client/Client.ts">update</a>({ ...params }) -> Evcloud.RoutingRuleOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Send ``expected_revision`` to refuse the write (409) if the row changed since you read it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.routingRules.update({
    routing_rule_id: "5b2f8d4e-1a3c-4e6f-8b7d-9c0a1e2f3b4d",
    priority: 200
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.RoutingRuleUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `RoutingRulesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy ChargerPoints
<details><summary><code>client.proxy.chargerPoints.<a href="/src/api/resources/proxy/resources/chargerPoints/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.ChargerPointOut, Evcloud.ChargerPointPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Chargers registered with the proxy, with their security profile and last authentication failure.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.chargerPoints.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.chargerPoints.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListChargerPointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargerPointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.chargerPoints.<a href="/src/api/resources/proxy/resources/chargerPoints/client/Client.ts">get</a>({ ...params }) -> Evcloud.ChargerPointOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One charger registered with the proxy. Passwords and certificates are never returned, only whether they are set.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.chargerPoints.get({
    charge_point_id: "CP-AMS-001"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetChargerPointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargerPointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.chargerPoints.<a href="/src/api/resources/proxy/resources/chargerPoints/client/Client.ts">update</a>({ ...params }) -> Evcloud.ChargerPointOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Change its label, hardware details or metadata, or disable it (``enabled: false``: the proxy refuses its connection). Send ``expected_revision`` to refuse the write (409) if it changed since you read it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.chargerPoints.update({
    charge_point_id: "CP-AMS-001",
    label: "Amsterdam lot, bay 1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ChargerPointUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargerPointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy Fleet
<details><summary><code>client.proxy.fleet.<a href="/src/api/resources/proxy/resources/fleet/client/Client.ts">get</a>({ ...params }) -> Evcloud.FleetOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Counts your chargers by security profile and lists the ones that are not ready: still on profile 0, missing a password or client certificate pin, or not seen recently. ``ready`` is true when every list is empty.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.fleet.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetFleetRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FleetClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy ChargeSessions
<details><summary><code>client.proxy.chargeSessions.<a href="/src/api/resources/proxy/resources/chargeSessions/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.ChargeSessionOut, Evcloud.ChargeSessionPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

WebSocket connections your chargers opened to the proxy, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.chargeSessions.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.chargeSessions.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListChargeSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargeSessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.chargeSessions.<a href="/src/api/resources/proxy/resources/chargeSessions/client/Client.ts">get</a>({ ...params }) -> Evcloud.ChargeSessionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One charger connection to the proxy.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.chargeSessions.get({
    charge_session_id: "charge_session_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetChargeSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ChargeSessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy BackendSessions
<details><summary><code>client.proxy.backendSessions.<a href="/src/api/resources/proxy/resources/backendSessions/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.BackendSessionOut, Evcloud.BackendSessionPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Connections the proxy opened to your backends on behalf of a charger, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.backendSessions.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.backendSessions.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListBackendSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendSessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.backendSessions.<a href="/src/api/resources/proxy/resources/backendSessions/client/Client.ts">get</a>({ ...params }) -> Evcloud.BackendSessionOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One connection the proxy opened to a backend.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.backendSessions.get({
    backend_session_id: "backend_session_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetBackendSessionsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BackendSessionsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy FrameLogs
<details><summary><code>client.proxy.frameLogs.<a href="/src/api/resources/proxy/resources/frameLogs/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.FrameLogOut, Evcloud.FrameLogPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Frames the proxy relayed between your chargers and backends, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.frameLogs.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.frameLogs.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListFrameLogsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FrameLogsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.frameLogs.<a href="/src/api/resources/proxy/resources/frameLogs/client/Client.ts">get</a>({ ...params }) -> Evcloud.FrameLogOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One frame, with its full payload.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.frameLogs.get({
    frame_log_id: "frame_log_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.GetFrameLogsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FrameLogsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Proxy Configuration
<details><summary><code>client.proxy.configuration.<a href="/src/api/resources/proxy/resources/configuration/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.ConfigurationOut, Evcloud.ConfigurationPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

OCPP configuration keys the proxy stores for your chargers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.proxy.configuration.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.proxy.configuration.list();
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ListConfigurationRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConfigurationClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.proxy.configuration.<a href="/src/api/resources/proxy/resources/configuration/client/Client.ts">update</a>({ ...params }) -> Evcloud.ConfigurationOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin only. Sets the value the proxy stores for one charger's key; ``value: null`` clears it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.proxy.configuration.update({
    charge_point_id: "CP-AMS-001",
    key: "HeartbeatInterval",
    value: "300"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.proxy.ConfigurationUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConfigurationClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks Events
<details><summary><code>client.webhooks.events.<a href="/src/api/resources/webhooks/resources/events/client/Client.ts">deliver</a>({ ...params }) -> Evcloud.DeliverEventResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin tokens only: deliveries carry the platform signature. Queues one signed delivery per ACTIVE subscription of the event type. ``data`` must match the event type's payload schema. Posting the same ``event_id`` again queues nothing new.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.events.deliver({
    event: "energy.connector_status",
    data: {
        asset_id: "CP-AMS-001",
        asset_type: "CHARGEBOX",
        connector_id: 1,
        status: "Charging",
        timestamp: "2026-10-03T10:00:00Z"
    },
    occurred_at: "2026-10-03T10:00:00Z",
    event_id: "evt_2026-10-03_cp-ams-001_1"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.DeliverEventRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EventsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks Health
<details><summary><code>client.webhooks.health.<a href="/src/api/resources/webhooks/resources/health/client/Client.ts">get</a>() -> Evcloud.HealthOk</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Answers ``ok`` when the webhook gateway is up.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.health.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.health.<a href="/src/api/resources/webhooks/resources/health/client/Client.ts">queue</a>() -> Evcloud.QueueHealth</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Admin tokens only: covers every workspace. Pending and due deliveries and how long the oldest due one has waited. A growing ``oldest_due_seconds`` means deliveries are running behind.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.health.queue();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks Deliveries
<details><summary><code>client.webhooks.deliveries.<a href="/src/api/resources/webhooks/resources/deliveries/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.WebhookDeliveryResponse, Evcloud.WebhookDeliveryPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One row per attempt, retries included, newest first: the URL called and what your endpoint answered.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.webhooks.deliveries.list({
    offset: 0,
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.webhooks.deliveries.list({
    offset: 0,
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.ListDeliveriesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `DeliveriesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks EventTypes
<details><summary><code>client.webhooks.eventTypes.<a href="/src/api/resources/webhooks/resources/eventTypes/client/Client.ts">list</a>() -> Evcloud.EventTypeList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every event you can subscribe to, with its payload schema per ``api_version``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.eventTypes.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `EventTypesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.eventTypes.<a href="/src/api/resources/webhooks/resources/eventTypes/client/Client.ts">get</a>({ ...params }) -> Evcloud.EventTypeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Its payload versions, each with the JSON schema of the envelope ``data``.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.eventTypes.get({
    type: "energy.connector_status"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.GetEventTypesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EventTypesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks Endpoints
<details><summary><code>client.webhooks.endpoints.<a href="/src/api/resources/webhooks/resources/endpoints/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Evcloud.WebhookResponse, Evcloud.WebhookPage&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Your workspace's subscriptions. Secrets and custom header values are never returned.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.webhooks.endpoints.list({
    event_types: ["energy.connector_status"],
    offset: 0,
    limit: 50
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.webhooks.endpoints.list({
    event_types: ["energy.connector_status"],
    offset: 0,
    limit: 50
});
while (page.hasNextPage()) {
    page = page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.ListEndpointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EndpointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.endpoints.<a href="/src/api/resources/webhooks/resources/endpoints/client/Client.ts">create</a>({ ...params }) -> Evcloud.WebhookWithSecretResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The URL must be HTTPS and resolve to a public address. The signing secret is returned once, in this response; store it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.endpoints.create({
    name: "Connector status",
    description: "Live status for the operations dashboard",
    url: "https://hooks.example.com/ev-cloud",
    event: "energy.connector_status",
    custom_headers: {
        "X-Api-Key": "your-key"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.WebhookCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EndpointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.endpoints.<a href="/src/api/resources/webhooks/resources/endpoints/client/Client.ts">get</a>({ ...params }) -> Evcloud.WebhookResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Its delivery state and counters. The signing secret is never returned.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.endpoints.get({
    id: 9
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.GetEndpointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EndpointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.endpoints.<a href="/src/api/resources/webhooks/resources/endpoints/client/Client.ts">delete</a>({ ...params }) -> void</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deliveries stop immediately and the subscription's delivery history is removed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.endpoints.delete({
    id: 9
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.DeleteEndpointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EndpointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.endpoints.<a href="/src/api/resources/webhooks/resources/endpoints/client/Client.ts">update</a>({ ...params }) -> Evcloud.WebhookWithSecretResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Pause or resume it (resuming clears ``failure_count``), change its URL or headers, or rotate the secret (the new one is returned once).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.endpoints.update({
    id: 9,
    status: "PAUSED",
    rotate_secret: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.WebhookUpdateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EndpointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.endpoints.<a href="/src/api/resources/webhooks/resources/endpoints/client/Client.ts">test</a>({ ...params }) -> Evcloud.WebhookTestResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends one signed sample event of the subscription's type now. It is not retried, and the failure counters are not changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.endpoints.test({
    id: 9
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Evcloud.webhooks.TestEndpointsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EndpointsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

