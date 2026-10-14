Version: NAFATH-V2
Track: Software

## Overview
A telecom operator is starting a 5G service for emergency responders. Six IT fields collaborate to ensure this service stays dependable during network congestion, outages, and cyber attacks. Software controls HTTP requests and avoids issues when failed requests are retried. AI forecasts network congestion with machine learning models. Mobile applications enable responders to keep working offline and sync data when the connection is back. Networking employs 5G network slicing to assist critical communication. Cybersecurity aids in identifying attacks, securing the service, and restoring normal functions. Data systems compile daily service usage reports for various regions. Collectively, these six fields enhance service reliability, support quicker decisions, and assist emergency teams in communicating during tough situations.
## Software
GET, HEAD, OPTIONS, and TRACE are HTTP safe methods, which retrieve information without requesting changes from the server. Idempotent methods include GET, HEAD, OPTIONS, TRACE, PUT, and DELETE because repeating the same request has the same intended effect as sending it once. In general, POST is not idempotent. Automatic retries must be handled carefully because repeating a non-idempotent request may create duplicate records or actions.

Resource: RFC 9110 - HTTP Semantics - https://www.rfc-editor.org/rfc/rfc9110
## AI
Overfitting occurs when a machine learning model becomes too attached to the training data, including noise, and does not do well on new data. Cross-validation aids in identifying this by evaluating the model on various validation sets. For forecasting 5G network congestion, the operator should maintain the sequence of data during validation. This ensures a better prediction of future congestion rather than just succeeding on previous data.

Resource: Evaluating Time Series Forecasting Models: An Empirical Study on Performance Estimation Methods - https://arxiv.org/abs/1905.11744
## Mobile
The emergency responder's mobile app should continue working when the internet connection is lost. Important information and new reports should be saved in a local database on the device. When the connection returns, the app should synchronize the local data with the remote server. It should also check for duplicate reports and conflicting updates to protect data accuracy. This approach helps responders record important information during network outages without losing their work.

Resource: Synchronization Between Local and Remote Database on The Example of The Mobile Application of The Idvictim System - https://ibimapublishing.com/p-articles/40ICT/2022/4042522/

## Networking
With 5G network slicing, telecom operators can create logical networks using shared infrastructure. Each slice can support different service requirements, such as low latency, reliability, or high data capacity. For emergency responders, the operator can assign suitable network resources to support critical communication during congestion. This helps emergency teams communicate more effectively. It is important to have backup communication options in case of a network outage, yet network slicing cannot prevent every outage.

Resource: Conceptual Evaluation of a 5G Network Slicing Technique for Emergency Communications and Preliminary Estimate of Energy Trade-Off - https://www.mdpi.com/1996-1073/14/21/6876

## Cybersecurity
Cybersecurity incident response helps the operator manage attacks that threaten the emergency 5G service. According to NIST guidelines, preparation supports effective detection, response, and recovery. A first step in investigating an incident is identifying suspicious activity. Once the threat has been contained, the security team takes action to reduce its impact. Then, affected services are safely restored. Afterward, the team reviews lessons learned and improves security practices. These activities help reduce disruption and protect critical communication services.

Resource: NIST SP 800-61 Rev. 3 - Incident Response Recommendations and Considerations for Cybersecurity Risk Management - https://csrc.nist.gov/pubs/sp/800/61/r3/final

## Data
A star schema has a main fact table linked directly to dimension tables. A snowflake schema breaks some dimensions into smaller related tables, which can lower repeated data but might need more joins. For daily 5G service usage reports by area, I would pick a star schema since it is easier for reporting. A usage fact table connected to date and area dimensions would assist the operator in calculating daily traffic, comparing areas, and understanding service demand.

Resource: Performance of NoSQL Graph Implementations of Star vs. Snowflake Schemas - https://doi.org/10.1109/ACCESS.2022.3171256

## Misconception in My Track
A common misunderstanding is that safe and idempotent HTTP methods are identical. This is wrong. Safe methods are designed for getting information without making changes to the server. Idempotent methods can modify data, but repeating the same request produces the same result as sending it just once. For instance, DELETE is idempotent but not safe. This distinction is important because emergency applications might resend requests when connections are lost, and developers need to prevent unintentional duplicate actions.

## Open Question
How can emergency mobile applications safely retry HTTP POST requests when a network connection fails? I would investigate whether idempotency keys and server-side duplicate detection can prevent repeated actions while ensuring that important emergency reports are not lost.

