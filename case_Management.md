# Understanding Case Management Framework Implementation
Case Management bring a lot of functionality to BPM but all the implementation capabilities are not that obvious. We created this lab to illustrate this implementation methodology. 

This slide below is a good illustration of such an implementation. 

![build_project](images/buildproject/8.png)

In this implementation we created is a solution that makes use of both long running processes as well as short lived processes. We have some customers that used base short lived processes (Case Actions and/or Business Services) for their entire banking fraud management back office solution. One thing that short lived processes does not do is managing SLA's/Timer Events that ensures work gets done in a predefined time. 

Case Management provides a lot of flexibility to the normal BPM solution. 