+++
# Date this page was created.
date = 2016-04-27T00:00:00

# Project title.
title = "Optimizing Course Scheduling"

# Project summary to display on homepage.
summary = "A MIP-based Approach to Optimizing Course Scheduling at USC Marshall"

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "usc_marshall.jpg"


# Tags: can be used for filtering projects.
# Example: `tags = ["Optimization"]`
tags = ["Optimization"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to static/img/ folder).
[header] 
  image = "marshall_logo.jpg"

# Call to action button (optional).
#   Activate the button by specifying a URL and button label below.
#   Deactivate by commenting out parameters, prefixing lines with `#`.
[cta]
  url = "https://drive.google.com/open?id=1elzuswEmnR90O2PtxWdz5sA6r9LwuAKa"
  label = '<i class="fa fa-download"></i> Download the full report here'
+++

##### Executive Summary

For several universities across the world, the implementation of a systematic approach
to course scheduling remains a problem. Discrete optimization approaches have been
used to solve the problem independently at such institutions, however owing to the
complex nature of the problem compounded by the viewpoints of various
stakeholders, a universal “cookie-cutter” solution does not exist. There are 7
departments in the Marshall School of Business at USC, and course scheduling is
currently performed by reusing the course schedule from the previous year as closely
as possible and manually implementing a series of reforms to improve efficiency and
transparency. The current process assigns over 400 courses into 45 schedulable
rooms at 42 different times. However, the schedules produced by the current process
are not always transparent and efficient. Additionally, sections are scheduled and
de-scheduled multiple times during the course allotment process which makes greedy
approaches to the allocation problem inefficient.

Our solution to the problem involves the creation of a tractable MIP-based allocation
tool that equitably assigns departments to classroom-timeslots. An algorithm [1]
developed in-house generates classroom-timeslot preference scores for each
department based on survey results [2] , and every run of the allocation tool outputs
candidate sets of classroom-timeslots for each department. The size of the candidate
sets is dependent upon a model-tuning parameter that controls the greediness of the
allocation approach. This grants a greater degree of flexibility in course-scheduling and
ensures that a certain quantity of classroom-timeslots of each category [3] are available
for the next (potential) run of the allocation tool to assign the remaining sections. The
focus of this report is to describe the functioning of the tool, and the business value it
offers to the administrative wing of the Marshall School of Business.

In the first step of the report, we propose a precise and high-level explanation on how
the application of Mixed Integer Programming can be used to solve the course
scheduling problem. In the second step of the report, we formulate a Mixed Integer
Program by creating the input and output data, the decision variables, the objective
function and the constraints. We conclude with a description of the output from one
run of the model, and why the model makes sense and is easily implementable.


<a href="https://drive.google.com/open?id=115TjqrvSDv8hPvKhm-iOd1-nWNCgRRGw" download>Click to Download the full report</a>
