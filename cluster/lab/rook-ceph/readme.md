To get the rook dashboard to show up, I need to run this in a ceph toolbox

    ceph config set mgr mgr/dashboard/ssl false


echo admin | ceph dashboard set-login-credentials admin -i -
# ceph mgr module disable dashboard
# ceph mgr module enable dashboard
