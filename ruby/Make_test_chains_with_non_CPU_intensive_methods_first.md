# Always make test chains with non CPU intensive methods first

The simplest way to spare CPU cycle is to not run CPU intense method. So instead of writing a test like this:

    created_at > 1.day.ago and visible.nil?

Prefer the opposite test:

    visible.nil? and created_at > 1.day.ago 

Because `1.day.ago` = 3 ruby objects created (Integer -> Timing -> DateTime + compute time between current time), and if visible is nil, there's no need to compute time.
