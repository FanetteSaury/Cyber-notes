#THM #PreSecurity

| Parameter      | [[OSI Model]]                                                                      | [[TCP IP Model]]                                                                                    |
| -------------- | ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Full form      | Open Systems Interconnection                                                       | Transport Control Protocol / Internet Protocol                                                      |
| Layers         | 7                                                                                  | 4                                                                                                   |
| Usage          | Reference model to understand and design networks, but not implemented directly    | Practical model forming the basis of the internet                                                   |
| Approach       | Rigid architecture of layers communicating with the others                         | Flexible architecture, layers not as rigidly separated                                              |
| Error Handling | Present at the Data Link (frame errors) + Transport layer (end-to-end reliability) | Mainly the job of TCP, while UDP is stateless                                                       |
| Development    | ISO, late 1970s to build a communication standard                                  | Developed by DARPA (U.S. Defense) in the 1970s for building the ARPANET (precursor to the Internet) |
![[osi-model 3.gif]]